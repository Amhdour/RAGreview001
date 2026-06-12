# Final findings

## 1) Browser auth is cookie-based and the cookie name is shared across backend and frontend
- **Status:** confirmed
- **Evidence:** The backend cookie transport uses `FASTAPI_USERS_AUTH_COOKIE_NAME`/`AUTH_COOKIE_NAME`, and the frontend reads the same value as `SERVER_SIDE_ONLY__AUTH_COOKIE_NAME`. 【F:backend/onyx/configs/constants.py†L34-L43】【F:web/src/lib/constants.ts†L33-L39】【F:backend/onyx/auth/users.py†L1296-L1300】
- **Impact:** Browser login state is tied to a configurable cookie name rather than an implicit hard-coded value.
- **Client-ready wording:** The app keeps browser sessions in a shared, configurable auth cookie so the frontend and backend agree on the same session identifier.

## 2) BASIC and CLOUD users are subject to email verification, while SAML/OIDC users are treated as externally verified
- **Status:** confirmed
- **Evidence:** `user_needs_to_be_verified()` is true only for BASIC and CLOUD, `double_check_user()` blocks unverified users when required, and invite checks are bypassed for SAML/OIDC. 【F:backend/onyx/auth/users.py†L221-L227】【F:backend/onyx/auth/users.py†L247-L283】【F:backend/onyx/auth/users.py†L1908-L1938】
- **Impact:** Verification policy is deployment-type dependent, not global.
- **Client-ready wording:** Password-based users must verify their email when the workspace requires it, but SSO users are accepted as already verified by the identity provider.

## 3) OAuth, OIDC, and SAML login flows are explicitly wired and redirect back through the frontend
- **Status:** confirmed
- **Evidence:** The frontend builds provider-specific authorize URLs, the backend registers the corresponding routers, and the SAML callback wrapper forwards cookies and sanitizes relay state. 【F:web/src/lib/userSS.ts†L69-L124】【F:backend/onyx/main.py†L596-L673】【F:web/src/app/auth/saml/callback/route.ts†L10-L76】
- **Impact:** There is a clear, provider-specific login path for each supported SSO family.
- **Client-ready wording:** The repository supports separate login flows for Google OAuth, OIDC, and SAML, and each flow returns the user to the app through the frontend callback layer.

## 4) PATs and API keys are distinct bearer-token auth paths with different prefixes and request rules
- **Status:** confirmed
- **Evidence:** PATs use `onyx_pat_` and require bearer auth; API keys use `on_` with deprecated `dn_` support and accept bearer or raw token format. 【F:backend/onyx/auth/constants.py†L3-L15】【F:backend/onyx/auth/pat.py†L1-L43】【F:backend/onyx/auth/api_key.py†L1-L32】【F:backend/onyx/auth/utils.py†L16-L55】
- **Impact:** Non-browser auth is split into separate token families with different handling rules.
- **Client-ready wording:** Service tokens are not all the same: personal access tokens and API keys are minted, stored, and parsed through separate code paths.

## 5) Private route protection is enforced in two places: frontend layouts and backend auth checking
- **Status:** confirmed
- **Evidence:** `/app` uses `requireAuth()`, `/admin` uses `requireAdminAuth()`, and the backend route checker rejects private routes unless they carry a recognized auth dependency. 【F:web/src/app/app/layout.tsx†L15-L37】【F:web/src/layouts/admin/Layout.tsx†L11-L25】【F:backend/onyx/server/auth_check.py†L109-L163】【F:backend/onyx/main.py†L727-L728】
- **Impact:** Route protection is layered, so a frontend guard does not replace backend authorization checks.
- **Client-ready wording:** The app protects private pages in the browser and also verifies backend routes at the API layer.

## 6) Admin access is not a single gate; some routes are full-admin only, while others allow curator/admin roles
- **Status:** confirmed
- **Evidence:** Full admin-panel access protects user-role changes, accepted-user listing, and API-key management; OAuth config management allows curator/admin roles; the frontend admin layout allows `ADMIN`, `CURATOR`, and `GLOBAL_CURATOR`. 【F:backend/onyx/server/manage/users.py†L137-L203】【F:backend/onyx/server/api_key/api.py†L20-L62】【F:backend/onyx/server/features/oauth_config/api.py†L36-L149】【F:web/src/lib/auth/requireAuth.ts†L74-L119】
- **Impact:** Admin capability is role-specific and route-specific.
- **Client-ready wording:** Some admin tools are reserved for full admins, while others are intentionally available to curator-level roles.

## 7) External JWT bearer login is supported and can provision users automatically
- **Status:** confirmed
- **Evidence:** The backend looks for a Bearer JWT when `JWT_PUBLIC_KEY_URL` is configured, validates it, extracts an email claim, and creates or reuses a verified web-login user. 【F:backend/onyx/auth/users.py†L1666-L1786】【F:backend/onyx/configs/app_configs.py†L267-L304】
- **Impact:** The repository includes a separate bearer-token login path beyond PATs and API keys.
- **Client-ready wording:** Onyx can accept identity-provider JWTs directly and turn them into application users when the public key URL is configured.

## 8) Session refresh behavior differs by auth backend, and JWT sessions cannot be server-invalidated
- **Status:** confirmed
- **Evidence:** Redis sessions are stored in Redis and deleted on logout, DB sessions update expiration in the database, and JWT sessions are stateless with a no-op destroy function. 【F:backend/onyx/auth/users.py†L1319-L1488】
- **Impact:** Logout and invalidation semantics depend on which session backend is configured.
- **Client-ready wording:** Browser session invalidation works differently depending on whether the workspace uses Redis, Postgres, or stateless JWT sessions.

## 9) Verification and invite tests exist, but logout-cookie clearing was not directly asserted in a test file I reviewed
- **Status:** unverified
- **Evidence:** The implementation clears the cookie, but I did not locate a direct test for that exact browser-side outcome. 【F:web/src/app/auth/logout/route.ts†L15-L42】
- **Impact:** There is a small coverage gap around the logout side effect itself.
- **Client-ready wording:** Logout is implemented, but I did not find a test that proves the browser cookie is explicitly cleared end to end.
