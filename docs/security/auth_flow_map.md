> This is the client-facing mirror of the PHASE 5 evidence file. The canonical evidence copy remains under rag-security-readiness-review/02_evidence/phase_5/.

# PHASE 5 Authentication Flow Map

## 1. Purpose
This map identifies authentication entry points, user-session dependencies, token/cookie handling evidence, and frontend auth screens using repository files only.

## 2. Scope
- In scope: `backend/onyx/auth/`, `backend/onyx/server/auth/`, `backend/onyx/server/saml.py`, `backend/onyx/main.py`, `backend/onyx/server/pat/api.py`, `web/src/app/auth/`, `web/src/app/api/[...path]/route.ts`, and auth-related frontend helpers under `web/src/app/auth/`.
- Out of scope: identity-provider configuration outside repository files, live session state, production cookie attributes not visible in code/config, and authentication claims not backed by files.

## 3. Main entry points
- Backend auth setup: `backend/onyx/main.py`.
- User manager/auth backends/current-user dependencies: `backend/onyx/auth/users.py`.
- JWT helpers: `backend/onyx/auth/jwt.py`.
- API key helpers: `backend/onyx/auth/api_key.py`, `backend/onyx/server/api_key/api.py`.
- Personal access token helpers/routes: `backend/onyx/auth/pat.py`, `backend/onyx/server/pat/api.py`, `backend/onyx/db/pat.py`.
- OAuth token helpers: `backend/onyx/auth/oauth_token_manager.py`, `backend/onyx/auth/oauth_refresher.py`, `backend/onyx/server/documents/standard_oauth.py`, `backend/onyx/server/features/oauth_config/api.py`.
- SAML route file: `backend/onyx/server/saml.py`.
- Captcha auth middleware/routes: `backend/onyx/server/auth/captcha_api.py`.
- Frontend auth pages/routes: `web/src/app/auth/login/page.tsx`, `web/src/app/auth/logout/route.ts`, `web/src/app/auth/signup/page.tsx`, `web/src/app/auth/forgot-password/page.tsx`, `web/src/app/auth/reset-password/page.tsx`, `web/src/app/auth/verify-email/page.tsx`.

## 4. Architecture flow
1. `backend/onyx/main.py` imports auth schemas, auth backend objects, FastAPI Users routers, OAuth clients, SAML router, captcha router, and auth middleware.
2. `backend/onyx/auth/users.py` defines user-management/authentication dependencies and imports cookie/JWT/database auth strategy classes from FastAPI Users.
3. API key and PAT authentication paths are represented by `backend/onyx/auth/api_key.py`, `backend/onyx/auth/pat.py`, `backend/onyx/server/api_key/api.py`, and `backend/onyx/server/pat/api.py`.
4. OAuth/OIDC/SAML paths are represented by OAuth imports and router registration in `backend/onyx/main.py`, helper modules in `backend/onyx/auth/`, document OAuth routes in `backend/onyx/server/documents/standard_oauth.py`, OAuth config routes in `backend/onyx/server/features/oauth_config/api.py`, and SAML routes in `backend/onyx/server/saml.py`.
5. Frontend login, logout, signup, password reset, and email verification screens/routes are under `web/src/app/auth/`.

## 5. Supporting evidence
- `backend/onyx/main.py` — imports and registers auth-related routers and middleware.
- `backend/onyx/auth/users.py` — user manager, auth backend, current-user dependencies, cookie/JWT/database strategy imports, anonymous user helper.
- `backend/onyx/auth/jwt.py` — JWT token verification helper.
- `backend/onyx/auth/api_key.py`, `backend/onyx/server/api_key/api.py` — API key auth helpers and route module.
- `backend/onyx/auth/pat.py`, `backend/onyx/db/pat.py`, `backend/onyx/server/pat/api.py` — personal access token helpers, DB access, and route module.
- `backend/onyx/auth/oauth_token_manager.py`, `backend/onyx/auth/oauth_refresher.py`, `backend/onyx/server/features/oauth_config/api.py`, `backend/onyx/server/documents/standard_oauth.py` — OAuth-related backend files.
- `backend/onyx/server/saml.py` — SAML authorize/callback/logout route file.
- `backend/onyx/server/auth/captcha_api.py` — captcha route/middleware file.
- `web/src/app/auth/` — frontend auth screens and logout route.

## 6. Dependencies
- Internal dependencies: auth code depends on DB auth/user/PAT helpers in `backend/onyx/db/`, app config constants in `backend/onyx/configs/`, and server route registration in `backend/onyx/main.py`.
- External dependencies supported by files: FastAPI Users imports in `backend/onyx/auth/users.py`; OAuth/OpenID client imports in `backend/onyx/main.py`; SAML route file in `backend/onyx/server/saml.py`.

## 7. Gaps / unknowns
- Actual enabled auth mode is configuration-dependent and not claimed without runtime environment values.
- Identity-provider tenant settings, live OAuth clients, and live SAML metadata are not available from repository source alone.

## 8. Client-ready summary
The repository supports several authentication-related code paths: browser user auth, API keys, personal access tokens, OAuth/OIDC, SAML, and captcha support. The backend registers these routes and dependencies, while the frontend provides login, logout, signup, password reset, and verification screens.

## Support table
| Claim | Evidence file paths | Support status | Notes |
|---|---|---:|---|
| Backend authentication setup is wired through the main application file. | `backend/onyx/main.py` | Supported | Auth routers, OAuth clients, and middleware imports appear there. |
| User session/current-user dependencies are defined in auth user code. | `backend/onyx/auth/users.py` | Supported | The file defines user management and current-user dependency objects. |
| Cookie/JWT/database auth strategies are represented in code. | `backend/onyx/auth/users.py`, `backend/onyx/auth/jwt.py` | Supported | Strategy imports and JWT helper file are present. |
| API keys and PATs are separate authentication surfaces. | `backend/onyx/auth/api_key.py`, `backend/onyx/server/api_key/api.py`, `backend/onyx/auth/pat.py`, `backend/onyx/server/pat/api.py` | Supported | Separate helper and route files exist. |
| OAuth/OIDC/SAML paths are represented in repository files. | `backend/onyx/main.py`, `backend/onyx/auth/oauth_token_manager.py`, `backend/onyx/server/features/oauth_config/api.py`, `backend/onyx/server/saml.py` | Supported | OAuth/OIDC/SAML files exist. |
| Frontend auth screens exist. | `web/src/app/auth/login/page.tsx`, `web/src/app/auth/logout/route.ts`, `web/src/app/auth/signup/page.tsx` | Supported | Auth route files exist. |
| A specific auth mode is enabled in production. | No repository evidence identified. | Unsupported | Runtime environment values are not established here. |

## Missing or unsupported items
- Production-enabled auth mode, identity-provider settings, and live session state are unsupported by repository files alone.
