# Authentication Risk to Code

## Category purpose
Map authentication risks to concrete Onyx files that appear to establish, refresh, store, or terminate identity and token state.

## Related PHASE 7 risks
- AUTH-01
- AUTH-02
- AUTH-03
- AUTH-04
- AUTH-05
- RAG-01
- RAG-02

## Related PHASE 6 threats
- TH-13
- TH-14

## Related PHASE 5 architecture evidence
- rag-security-readiness-review/02_evidence/phase_5/auth_flow_map.md
- rag-security-readiness-review/02_evidence/phase_5/api_routes_map.md
- rag-security-readiness-review/02_evidence/phase_5/backend_architecture.md
- rag-security-readiness-review/02_evidence/phase_5/frontend_architecture.md

## Related PHASE 3 inventory evidence
- rag-security-readiness-review/02_evidence/phase_3/baseline_inventory.md
- rag-security-readiness-review/02_evidence/phase_3/important_files_index.md
- rag-security-readiness-review/02_evidence/phase_3/security_relevant_files.md

## Candidate Onyx file paths
- backend/onyx/auth/jwt.py
- backend/onyx/auth/api_key.py
- backend/onyx/auth/pat.py
- backend/onyx/auth/oauth_token_manager.py
- backend/onyx/auth/oauth_refresher.py
- backend/onyx/auth/users.py
- backend/onyx/auth/utils.py
- backend/ee/onyx/server/oauth/api.py
- backend/ee/onyx/server/oauth/api_router.py
- web/src/app/auth/login/EmailPasswordForm.tsx
- web/src/app/auth/logout/route.ts
- web/src/app/auth/oauth/callback/route.ts
- web/src/app/auth/oidc/callback/route.ts
- web/src/app/auth/saml/callback/route.ts

## Existing control candidates
- AUTH-MAP-01: JWT, API key, PAT, and login entry points appear to exist.
- AUTH-MAP-02: OAuth/OIDC/SAML callback and token-refresh paths appear to exist.

## Missing control candidates
- No dedicated session revocation or replay-proof evidence path was confirmed.

## Unverified mappings
- AUTH-MAP-03: logout and user helpers do not validate session invalidation.

## Later validation methods
- Runtime token lifecycle validation.
- Logout and replay handling review.
- Federation callback validation.

## Non-claims
- No claim that authentication is secure or complete.
- No claim that token revocation is effective.

## Client-ready summary
The category links login, token, API-key, PAT, and federation surfaces to concrete code paths without claiming that they are effective controls.

## Mapping table

| Mapping ID | Related risk ID/category | Related PHASE 6 threat ID | Related PHASE 5 architecture evidence | Candidate Onyx file/path | Mapping label | Why this file/path matters | Missing evidence | Later validation method | Notes |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| AUTH-MAP-01 | AUTH-01 / RAG-01 | TH-13 | auth_flow_map.md; frontend_architecture.md | backend/onyx/auth/jwt.py; backend/onyx/auth/api_key.py; backend/onyx/auth/pat.py; web/src/app/auth/login/EmailPasswordForm.tsx | EXISTING-CANDIDATE | These paths hold the main credential issuance and login surfaces for bearer tokens, API keys, PATs, and password entry. | No runtime validation of token issuance, login hardening, or secret storage was performed. | Session, token, and API-key lifecycle validation; login and logout behavior review. | Source-only candidate; no effectiveness claim. |
| AUTH-MAP-02 | AUTH-02 / AUTH-04 | TH-13 / TH-14 | auth_flow_map.md; api_routes_map.md; frontend_architecture.md | backend/onyx/auth/oauth_token_manager.py; backend/onyx/auth/oauth_refresher.py; backend/ee/onyx/server/oauth/api.py; web/src/app/auth/oauth/callback/route.ts; web/src/app/auth/oidc/callback/route.ts; web/src/app/auth/saml/callback/route.ts | EXISTING-CANDIDATE | These files suggest the token-refresh and federation callback control points for OAuth, OIDC, and SAML sign-in flows. | No live identity-provider metadata or token refresh validation was performed. | Federation config review and callback-flow runtime validation. | Token refresh and callback paths appear present but unverified. |
| AUTH-MAP-03 | AUTH-03 / AUTH-05 | TH-13 / TH-14 | auth_flow_map.md; backend_architecture.md | backend/onyx/auth/users.py; backend/onyx/auth/utils.py; web/src/app/auth/logout/route.ts | UNVERIFIED | These files are consistent with account and logout handling, but they do not prove token revocation or replay resistance. | No runtime session replay, logout invalidation, or revocation evidence was collected. | Session/JWT replay testing and logout invalidation review. | Unverified because source-only evidence cannot confirm lifecycle behavior. |
