# User verification checks

## Confirmed rules
- `user_needs_to_be_verified()` returns the configured verification requirement only for BASIC and CLOUD auth types; other auth types return `False`. 【F:backend/onyx/auth/users.py†L221-L227】
- `double_check_user()` rejects an authenticated user whose `is_verified` flag is false when verification is required, and also rejects expired OIDC sessions when `oidc_expiry` has passed. 【F:backend/onyx/auth/users.py†L1908-L1938】
- The frontend mirrors that behavior: the login page sends verified users to `/app` but sends unverified users to `/auth/waiting-on-verification`. 【F:web/src/app/auth/login/page.tsx†L54-L69】

## Invite / domain / signup rules
- Invite-only enforcement is skipped entirely for SAML and OIDC in `verify_email_is_invited()`, but it remains active for other auth types when invite-only is enabled. 【F:backend/onyx/auth/users.py†L247-L283】
- `verify_email_domain()` rejects invalid formats, disposable domains, Googlemail addresses, dotted Gmail addresses on registration, and plus-addresses for cloud users outside `@onyx.app`. 【F:backend/onyx/auth/users.py†L292-L337】
- `UserManager.create()` applies disposable-email checks first, then signup rate limiting, then captcha validation, then invite-list enforcement. 【F:backend/onyx/auth/users.py†L505-L557】【F:backend/onyx/auth/users.py†L585-L596】

## External-auth user provisioning
- JWT bearer login provisions a user on first login, but only after invite/domain checks and only if the user is active and a web-login role. Existing users are reused, and the OIDC expiry is synchronized from the JWT `exp` claim when configured. 【F:backend/onyx/auth/users.py†L1714-L1767】【F:backend/onyx/auth/users.py†L1683-L1706】
- SAML login creates a user with `is_verified=True` and marks the first SAML user as admin; later SAML users are basic users. 【F:backend/onyx/server/saml.py†L51-L119】【F:backend/onyx/server/saml.py†L280-L284】

## Verification UI flow
- The verification email page posts to `/api/auth/verify` with the token query parameter and then returns the user to `/auth/login?verified=true` or `/auth/login?verified=true&first_user=true`. 【F:web/src/app/auth/verify-email/Verify.tsx†L21-L46】
- The waiting page lets a verified user request another verification email, and its “request new email” button posts to `/api/auth/request-verify-token`. 【F:web/src/app/auth/waiting-on-verification/page.tsx†L36-L56】【F:web/src/app/auth/waiting-on-verification/RequestNewVerificationEmail.tsx†L18-L39】【F:web/src/app/auth/lib.ts†L1-L10】

## Confirmed tests
- The unit tests assert the cloud-specific domain restrictions, including `googlemail.com`, plus-addressing, and dotted Gmail handling. 【F:backend/tests/unit/onyx/auth/test_verify_email_domain.py†L9-L106】
- The invite tests assert that SAML/OIDC bypass invite-only checks while BASIC auth still enforces them. 【F:backend/tests/unit/onyx/auth/test_verify_email_invite.py†L9-L41】
- The user-registration tests assert disposable-email blocking, tenant invite logic, and SSO bypass behavior. 【F:backend/tests/unit/onyx/auth/test_user_registration.py†L71-L147】【F:backend/tests/unit/onyx/auth/test_user_registration.py†L149-L297】【F:backend/tests/unit/onyx/auth/test_user_registration.py†L299-L416】
- The JWT provisioning tests assert that JWT login requires an email claim, skips inactive users, and provisions new users as verified. 【F:backend/tests/unit/onyx/auth/test_jwt_provisioning.py†L32-L252】

## Unverified risks
- I did not identify a direct test that asserts the `/auth/request-verify-token` endpoint’s backend email content or delivery outcome.
