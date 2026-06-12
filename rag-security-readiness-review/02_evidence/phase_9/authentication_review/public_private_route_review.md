# Public vs private route review

## Auth-check public list
- The auth checker explicitly exempts the following route/method pairs from its private-route auth requirement: `/health`, `/auth/type`, `/version`, `/versions`, `/auth/refresh`, `/auth/register`, `/auth/login`, `/auth/captcha/oauth-verify`, `/auth/logout`, `/auth/forgot-password`, `/auth/reset-password`, `/auth/request-verify-token`, `/auth/verify`, `GET /users/me`, `PATCH /users/me`, `GET /users/{id}`, `PATCH /users/{id}`, `DELETE /users/{id}`, `/auth/oauth/authorize`, `/auth/oauth/callback`, `/auth/oidc/authorize`, `/auth/oidc/callback`, `/auth/saml/authorize`, `/auth/saml/callback`, `/auth/saml/logout`, `/tenants/anonymous-user`, `/metrics`, and the build webapp proxy paths. 【F:backend/onyx/server/auth_check.py†L16-L72】
- The same file requires every other route to expose a recognized auth dependency, and `main.py` calls `check_router_auth(application)` after routes are registered. 【F:backend/onyx/server/auth_check.py†L109-L163】【F:backend/onyx/main.py†L727-L728】

## Backend private-route enforcement
- The checker treats `current_limited_user`, `current_user`, `current_curator_or_admin_user`, `current_user_with_expired_token`, `current_chat_accessible_user`, `current_user_from_websocket`, `require_permission(...)`, `control_plane_dep`, `current_cloud_superuser`, and `verify_scim_token` as valid auth dependencies. 【F:backend/onyx/server/auth_check.py†L118-L163】
- `require_permission()` enforces both the user’s stored permissions and any scoped token restrictions, and it can admit anonymous users only when the caller asks for that explicitly. 【F:backend/onyx/auth/permissions.py†L101-L128】
- `current_chat_accessible_user()` can return the anonymous user object when the tenant setting allows it. 【F:backend/onyx/auth/users.py†L1952-L1959】

## Frontend private-route enforcement
- The root app subtree is wrapped in `requireAuth()`, which redirects to `/auth/login` if the current user is missing and to `/auth/waiting-on-verification` if verification is still pending. 【F:web/src/app/app/layout.tsx†L15-L37】【F:web/src/lib/auth/requireAuth.ts†L36-L71】
- The admin subtree is wrapped in `requireAdminAuth()`, which redirects non-admin roles to `/app`. 【F:web/src/layouts/admin/Layout.tsx†L11-L25】【F:web/src/lib/auth/requireAuth.ts†L74-L119】
- The root route redirects to `/app`, so the private app layout is the default landing point. 【F:web/src/app/page.tsx†L1-L5】

## Public frontend auth pages
- `/auth/login` self-redirects existing authenticated users to `/app?from=login` or `/auth/waiting-on-verification`, and it auto-redirects OIDC/SAML users to the provider URL when configured. 【F:web/src/app/auth/login/page.tsx†L43-L83】
- `/auth/signup` and `/auth/join` both self-redirect authenticated users away from the public page, and both only allow BASIC or CLOUD flows. 【F:web/src/app/auth/signup/page.tsx†L44-L56】【F:web/src/app/auth/join/page.tsx†L45-L61】
- `/auth/forgot-password` and `/auth/reset-password` redirect to `/auth/login` when the feature is disabled or after successful reset. 【F:web/src/app/auth/forgot-password/page.tsx†L19-L24】【F:web/src/app/auth/reset-password/page.tsx†L39-L41】【F:web/src/app/auth/reset-password/page.tsx†L66-L74】

## Confirmed test coverage for route protection
- The browser auth tests exercise `/auth/login`, `/auth/signup`, `/auth/verify-email`, and the PAT page flow under a logged-in session. 【F:web/tests/e2e/auth/login.spec.ts†L11-L45】【F:web/tests/e2e/auth/signup.spec.ts†L7-L167】【F:web/tests/e2e/auth/email_verification.spec.ts†L7-L25】【F:web/tests/e2e/auth/pat_management.spec.ts†L11-L65】
- The backend permission tests assert that BASIC_ACCESS routes allow admin/basic users but reject anonymous, limited, bot, and external-permission principals. 【F:backend/tests/integration/tests/permissions/test_basic_access.py†L1-L153】

## Unverified risk
- I did not identify a file-level assertion that the generated backend routers for `GET /users/me` and `PATCH /users/me` still require auth at the handler layer in every deployment; the auth checker exempts them, so the actual protection depends on the included router implementation.
