> This is the client-facing mirror of the PHASE 7 evidence file. The canonical evidence copy remains under rag-security-readiness-review/02_evidence/phase_7/.

# Authentication Risks

## Category purpose

Track risks around identity establishment, token use, and federation configuration.

## Scope

API keys, PATs, session/JWT handling, and OAuth/OIDC/SAML flows.

## Related PHASE 5 architecture evidence

- rag-security-readiness-review/02_evidence/phase_5/auth_flow_map.md

## Related PHASE 6 threats

- TH-13
- TH-14

## Protected assets affected

API keys; PATs; session cookies; JWTs; OAuth/OIDC/SAML tokens

## Actors involved

API key user; PAT user; OAuth/OIDC/SAML identity; compromised user; deployment/operator role

## Trust boundaries involved

Authentication; federation; unauthenticated/authenticated; identity provider boundary

## Data flows involved

Credential presentation to auth endpoints; federated identity exchange; token issuance and reuse

## Risk list

| Risk ID | Risk | Evidence label | Related PHASE 6 threat ID | Related PHASE 5 evidence | Affected assets | Actors | Trust boundaries | Potential impact | Missing evidence | Later validation method | Priority |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| AUTH-01 | API key abuse can grant programmatic access without interactive login. | EVIDENCE-LINKED | TH-13 | auth_flow_map.md | API keys; PATs; session cookies; JWTs; OAuth/OIDC/SAML tokens | API key user; PAT user; OAuth/OIDC/SAML identity; compromised user; deployment/operator role | Authentication; federation; unauthenticated/authenticated; identity provider boundary | Unauthorized API access and account impersonation. | No live token lifecycle validation. | Later token-security review. | Critical candidate |
| AUTH-02 | PAT abuse can permit durable bearer-token misuse. | EVIDENCE-LINKED | TH-13 | auth_flow_map.md | API keys; PATs; session cookies; JWTs; OAuth/OIDC/SAML tokens | API key user; PAT user; OAuth/OIDC/SAML identity; compromised user; deployment/operator role | Authentication; federation; unauthenticated/authenticated; identity provider boundary | Token reuse can impersonate a user or persist after compromise. | No live PAT rotation or revocation review. | Later token-lifecycle review. | High candidate |
| AUTH-03 | Session or JWT misuse can keep a compromised identity active. | INFERRED | TH-13 | auth_flow_map.md | API keys; PATs; session cookies; JWTs; OAuth/OIDC/SAML tokens | API key user; PAT user; OAuth/OIDC/SAML identity; compromised user; deployment/operator role | Authentication; federation; unauthenticated/authenticated; identity provider boundary | Stolen session material may extend unauthorized access. | No runtime session validation or replay test. | Later session/JWT review. | High candidate |
| AUTH-04 | OAuth/OIDC/SAML misconfiguration could map identities incorrectly. | UNVERIFIED | TH-14 | auth_flow_map.md | API keys; PATs; session cookies; JWTs; OAuth/OIDC/SAML tokens | API key user; PAT user; OAuth/OIDC/SAML identity; compromised user; deployment/operator role | Authentication; federation; unauthenticated/authenticated; identity provider boundary | Wrong identity mapping or overbroad access. | No live IdP metadata or settings review. | Later federation-config review. | Medium candidate |
| AUTH-05 | Weak lifecycle around token issuance or revocation remains unverified. | UNVERIFIED | TH-13, TH-14 | auth_flow_map.md | API keys; PATs; session cookies; JWTs; OAuth/OIDC/SAML tokens | API key user; PAT user; OAuth/OIDC/SAML identity; compromised user; deployment/operator role | Authentication; federation; unauthenticated/authenticated; identity provider boundary | Expired or revoked credentials might remain usable. | No live token-issuance or revocation review. | Later lifecycle and federation review. | Medium candidate |

## Missing evidence

No live token lifecycle validation; no live IdP metadata or configuration review; no runtime auth mode confirmation.

## Later validation methods

Token lifecycle and revocation review; federation configuration review; live auth mode verification.

## Non-claims

No claim that auth controls are verified; no claim that identity takeover was demonstrated; no claim that federation is correctly configured.

## Client-ready summary

The category remains source-only and distinguishes confirmed token surfaces from unverified federation and lifecycle behavior.
