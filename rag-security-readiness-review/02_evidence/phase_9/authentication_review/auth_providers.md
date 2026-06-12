# Authentication provider matrix

## BASIC username/password
- Login is rendered on `/auth/login` and uses the email/password form when `authTypeMetadata.authType === AuthType.BASIC`. The page redirects logged-in users to `/app?from=login`, or to `/auth/waiting-on-verification` when verification is required and the user is still unverified. 【F:web/src/app/auth/login/page.tsx†L43-L83】【F:web/src/app/auth/login/LoginPage.tsx†L82-L87】
- Signup is exposed at `/auth/signup`, but only when auth type is BASIC or CLOUD. The page redirects authenticated users to `/app` or `/auth/waiting-on-verification`. 【F:web/src/app/auth/signup/page.tsx†L44-L56】
- The backend registers the standard fastapi-users auth/register/verify/reset routes for BASIC and CLOUD. 【F:backend/onyx/main.py†L567-L594】

## GOOGLE_OAUTH / CLOUD
- The frontend builds Google OAuth authorization URLs at `/api/auth/oauth/authorize` and uses the same Google authorize flow for CLOUD. 【F:web/src/lib/userSS.ts†L79-L118】
- The login page shows a Google sign-in button for CLOUD and, in CLOUD mode, keeps the email/password form as a fallback. 【F:web/src/app/auth/login/LoginPage.tsx†L57-L79】【F:web/src/app/auth/login/SignInButton.tsx†L53-L63】
- The backend only registers the Google OAuth router when auth type is GOOGLE_OAUTH or when BASIC has OAuth credentials configured; in CLOUD it still uses the Google OAuth authorize/callback flow plus the standard auth router. 【F:backend/onyx/main.py†L596-L630】

## OIDC
- The frontend builds the OIDC authorization URL at `/api/auth/oidc/authorize`. 【F:web/src/lib/userSS.ts†L69-L77】【F:web/src/lib/userSS.ts†L119-L124】
- The backend registers the OIDC router under `/auth/oidc` and also includes the standard `/auth` logout router. 【F:backend/onyx/main.py†L631-L667】
- `getAuthTypeMetadataSS()` marks OIDC as auto-redirecting when a user is unauthenticated. 【F:web/src/lib/userSS.ts†L45-L57】

## SAML
- The frontend gets the SAML authorize URL by calling `/auth/saml/authorize`, then redirects through the returned IdP URL. 【F:web/src/lib/userSS.ts†L89-L102】
- The backend exposes `/auth/saml/authorize`, `/auth/saml/callback` for GET and POST, and `/auth/saml/logout`. 【F:backend/onyx/server/saml.py†L35-L35】【F:backend/onyx/server/saml.py†L192-L297】
- The SAML callback wrapper in the frontend forwards the backend `Set-Cookie` header and sanitizes `RelayState` before redirecting. 【F:web/src/app/auth/saml/callback/route.ts†L10-L76】

## JWT bearer login
- If `JWT_PUBLIC_KEY_URL` is set, the backend checks an `Authorization: Bearer <JWT>` header, verifies the JWT, derives an email from `email`, `preferred_username`, or `upn`, and creates or reuses a web-login user. 【F:backend/onyx/auth/users.py†L1666-L1786】【F:backend/onyx/configs/app_configs.py†L267-L304】

## PAT
- PATs are separate from browser sessions. They use the `onyx_pat_` prefix, require a bearer header, and are accepted by the auth helper as a token-scoped path. 【F:backend/onyx/auth/constants.py†L8-L15】【F:backend/onyx/auth/pat.py†L1-L43】【F:backend/onyx/auth/utils.py†L16-L55】
- The PAT route namespace is `/user/pats`, and creation returns the raw token only once while listing and deletion operate on stored records. 【F:backend/onyx/server/pat/api.py†L26-L107】【F:backend/onyx/db/pat.py†L110-L200】

## API key
- API keys use the `on_` prefix, with deprecated `dn_` support, and can be supplied as bearer or raw token. 【F:backend/onyx/auth/constants.py†L3-L15】【F:backend/onyx/auth/api_key.py†L1-L32】【F:backend/onyx/auth/utils.py†L16-L55】
- The admin API-key route namespace is `/admin/api-key`, and creation returns the raw key once while the DB layer stores only the hash/display form. 【F:backend/onyx/server/api_key/api.py†L17-L62】【F:backend/onyx/db/api_key.py†L79-L137】【F:backend/onyx/db/api_key.py†L199-L228】

## Client-ready note
- The repository supports two browser login families (BASIC/CLOUD password login and OAuth/OIDC/SAML SSO), plus three bearer-token families for non-browser access (JWT bearer login, PATs, and API keys). 【F:backend/onyx/main.py†L567-L687】【F:backend/onyx/auth/users.py†L1666-L1786】【F:backend/onyx/auth/pat.py†L1-L43】【F:backend/onyx/auth/api_key.py†L1-L32】
