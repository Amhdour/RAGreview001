# Authorization Risks

## Category purpose

Capture access-control failures between authenticated identities and permitted resources or actions.

## Scope

Document routes, admin routes, tenant/group boundaries, and backend/frontend permission alignment.

## Related PHASE 5 architecture evidence

- rag-security-readiness-review/02_evidence/phase_5/api_routes_map.md
- rag-security-readiness-review/02_evidence/phase_5/authorization_flow_map.md
- rag-security-readiness-review/02_evidence/phase_5/data_model_map.md

## Related PHASE 6 threats

- TH-02
- TH-03
- TH-04

## Protected assets affected

Document metadata; document contents; admin settings; tenant context; permission grants

## Actors involved

Authenticated user; admin; compromised user; malicious insider

## Trust boundaries involved

Authorization; document ownership/access; user/admin; tenant/group

## Data flows involved

API request to authz decision; frontend intent to backend enforcement; tenant context propagation

## Risk list

| Risk ID | Risk | Evidence label | Related PHASE 6 threat ID | Related PHASE 5 evidence | Affected assets | Actors | Trust boundaries | Potential impact | Missing evidence | Later validation method | Priority |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| AUTHZ-01 | Broken authorization on document routes can expose contents or metadata. | EVIDENCE-LINKED | TH-03 | api_routes_map.md; authorization_flow_map.md; data_model_map.md | Document metadata; document contents; admin settings; tenant context; permission grants | Authenticated user; admin; compromised user; malicious insider | Authorization; document ownership/access; user/admin; tenant/group | Unauthorized read or mutation of documents. | No route-level validation. | Later document-route review. | Critical candidate |
| AUTHZ-02 | Broken authorization on admin routes can enable privileged actions. | EVIDENCE-LINKED | TH-04 | api_routes_map.md; authorization_flow_map.md; data_model_map.md | Document metadata; document contents; admin settings; tenant context; permission grants | Authenticated user; admin; compromised user; malicious insider | Authorization; document ownership/access; user/admin; tenant/group | Privilege escalation and broad system change. | No live permission matrix. | Later admin-route review. | Critical candidate |
| AUTHZ-03 | Permission mismatch between frontend and backend can confuse users and checks. | INFERRED | TH-03, TH-04 | api_routes_map.md; authorization_flow_map.md; data_model_map.md | Document metadata; document contents; admin settings; tenant context; permission grants | Authenticated user; admin; compromised user; malicious insider | Authorization; document ownership/access; user/admin; tenant/group | A screen may imply access that the backend does not consistently grant or deny. | No live backend/frontend alignment check. | Later frontend/backend authorization review. | Medium candidate |
| AUTHZ-04 | Tenant boundary confusion can leak data across tenant partitions. | INFERRED | TH-02 | api_routes_map.md; authorization_flow_map.md; data_model_map.md | Document metadata; document contents; admin settings; tenant context; permission grants | Authenticated user; admin; compromised user; malicious insider | Authorization; document ownership/access; user/admin; tenant/group | Cross-tenant or cross-group leakage. | No live tenant state review. | Later multi-tenant isolation review. | High candidate |
| AUTHZ-05 | Route-level authorization has not been validated across the document and admin surfaces. | UNVERIFIED | TH-03, TH-04 | api_routes_map.md; authorization_flow_map.md; data_model_map.md | Document metadata; document contents; admin settings; tenant context; permission grants | Authenticated user; admin; compromised user; malicious insider | Authorization; document ownership/access; user/admin; tenant/group | Some routes may still be under-tested or under-documented. | No route-by-route validation evidence. | Later route review. | Informational |

## Missing evidence

No route-by-route permission test; no live permission matrix review; no runtime backend/frontend alignment check.

## Later validation methods

Document-route authorization review; admin-route authorization review; tenant/group boundary verification.

## Non-claims

No claim that authorization controls are verified; no claim of production readiness; no claim that all route checks succeed.

## Client-ready summary

The category isolates document and admin control failures from broader retrieval or agent issues.
