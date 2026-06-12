# Login, signup, logout, and verification flow

## Login
- `/auth/login` is the primary browser login page. If auth metadata says OIDC or SAML, the page auto-redirects to the IdP authorize URL; otherwise it renders either the password form or the cloud Google OAuth fallback. 【F:web/src/app/auth/login/page.tsx†L43-L83】【F:web/src/app/auth/login/LoginPage.tsx†L43-L87】
- The email/password form posts to `/api/auth/login` for login and `/api/auth/register` followed by `/api/auth/login` for signup. The tests assert the exact request bodies and redirect/result behavior. 【F:web/src/app/auth/login/EmailPasswordForm.tsx†L86-L175】【F:web/src/app/auth/login/EmailPasswordForm.test.tsx†L31-L74】【F:web/src/app/auth/login/EmailPasswordForm.test.tsx†L120-L189】
- Login failures are surfaced as explicit form messages, including `LOGIN_BAD_CREDENTIALS` and `NO_WEB_LOGIN_AND_HAS_NO_PASSWORD`. 【F:web/src/app/auth/login/EmailPasswordForm.tsx†L157-L174】

## Signup
- `/auth/signup` is only enabled for BASIC or CLOUD auth types; authenticated users are redirected away. 【F:web/src/app/auth/signup/page.tsx†L44-L56】
- The signup form can request verification and then routes the user to `/auth/waiting-on-verification` after signup when verification is required. 【F:web/src/app/auth/login/EmailPasswordForm.tsx†L139-L156】
- Cloud signup may also present Google sign-in alongside the password form. 【F:web/src/app/auth/signup/page.tsx†L63-L109】

## Verification
- The verification page `/auth/verify-email` posts the token to `/api/auth/verify` and then redirects to `/auth/login?verified=true` or `/auth/login?verified=true&first_user=true`. 【F:web/src/app/auth/verify-email/page.tsx†L10-L29】【F:web/src/app/auth/verify-email/Verify.tsx†L21-L46】
- The waiting page `/auth/waiting-on-verification` redirects to `/auth/login` when there is no current user and to `/app` when verification is not required or has already succeeded. 【F:web/src/app/auth/waiting-on-verification/page.tsx†L13-L35】
- The login page surfaces the `verified=true` query parameter as a success message. 【F:web/src/app/auth/login/LoginPage.tsx†L37-L42】

## Logout
- The frontend logout route proxies to the appropriate backend logout endpoint and then explicitly clears the browser auth cookie with `Max-Age=0`, `HttpOnly`, and `SameSite=Lax`. 【F:web/src/app/auth/logout/route.ts†L5-L42】
- The logout helper uses `/auth/saml/logout` for SAML and `/auth/logout` for the other browser auth types. 【F:web/src/lib/userSS.ts†L128-L154】
- For SAML, the backend logout route uses the fastapi-users session token dependency and calls `auth_backend.logout(strategy, user, token)`. 【F:backend/onyx/server/saml.py†L287-L297】

## Client-ready note
- The browser flow is: login/signup page → credential or SSO authorize path → backend sets/refreshes the auth cookie → frontend redirects to `/app` or verification pages → logout clears the cookie on the frontend and calls the matching backend logout route. 【F:web/src/app/auth/login/page.tsx†L43-L83】【F:web/src/app/auth/logout/route.ts†L5-L42】【F:web/src/lib/userSS.ts†L142-L154】
