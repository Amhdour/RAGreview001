# Authorization Risk to Code

## Category purpose
Map authorization risks to route guards, permission helpers, tenant context handling, and frontend admin gating surfaces.

## Related PHASE 7 risks
- AUTHZ-01
- AUTHZ-02
- AUTHZ-03
- AUTHZ-04
- AUTHZ-05
- RAG-01
- RAG-02

## Related PHASE 6 threats
- TH-02
- TH-03
- TH-04

## Related PHASE 5 architecture evidence
- rag-security-readiness-review/02_evidence/phase_5/api_routes_map.md
- rag-security-readiness-review/02_evidence/phase_5/authorization_flow_map.md
- rag-security-readiness-review/02_evidence/phase_5/data_model_map.md
- rag-security-readiness-review/02_evidence/phase_5/frontend_architecture.md

## Related PHASE 3 inventory evidence
- rag-security-readiness-review/02_evidence/phase_3/baseline_inventory.md
- rag-security-readiness-review/02_evidence/phase_3/important_files_index.md
- rag-security-readiness-review/02_evidence/phase_3/security_relevant_files.md

## Candidate Onyx file paths
- backend/onyx/auth/permissions.py
- backend/onyx/hooks/api_dependencies.py
- backend/onyx/server/features/persona/api.py
- backend/ee/onyx/server/auth_check.py
- backend/ee/onyx/server/user_group/api.py
- backend/ee/onyx/db/user_group.py
- web/src/app/admin/layout.tsx
- web/src/app/admin/users/page.tsx
- web/src/app/admin/groups/page.tsx

## Existing control candidates
- AUTHZ-MAP-01: permission helper and dependency-based control points appear present.
- AUTHZ-MAP-02: server-side user-group and auth-check paths appear present.

## Missing control candidates
- No dedicated route-by-route authorization audit evidence was identified.

## Unverified mappings
- Frontend admin gating exists as a candidate but is not runtime validated.

## Later validation methods
- Route-level authorization testing.
- Tenant isolation validation.
- Frontend/backend permission alignment review.

## Non-claims
- No claim of complete access-control correctness.
- No claim of validated tenant isolation.

## Client-ready summary
The category highlights the files most likely to enforce permissions, but the current pass only establishes source-level candidates.

## Mapping table

| Mapping ID | Related risk ID/category | Related PHASE 6 threat ID | Related PHASE 5 architecture evidence | Candidate Onyx file/path | Mapping label | Why this file/path matters | Missing evidence | Later validation method | Notes |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| AUTHZ-MAP-01 | AUTHZ-01 / RAG-01 | TH-03 | api_routes_map.md; authorization_flow_map.md; data_model_map.md | backend/onyx/auth/permissions.py; backend/onyx/hooks/api_dependencies.py; backend/onyx/server/features/persona/api.py; web/src/app/admin/layout.tsx | EXISTING-CANDIDATE | These paths are the clearest local evidence for permission helpers, dependency-based checks, and admin navigation gating. | No live route-by-route authorization test was performed. | Document-route authorization review and admin-route boundary review. | Candidate enforcement points only; no validation claim. |
| AUTHZ-MAP-02 | AUTHZ-02 / AUTHZ-04 | TH-02 / TH-04 | api_routes_map.md; authorization_flow_map.md; data_model_map.md | backend/ee/onyx/server/auth_check.py; backend/ee/onyx/server/user_group/api.py; backend/ee/onyx/db/user_group.py; web/src/app/admin/users/page.tsx; web/src/app/admin/groups/page.tsx | EXISTING-CANDIDATE | These files suggest server-side checks and group-aware authorization data used for tenant or admin decisions. | No live permission-matrix inspection or tenant-isolation runtime evidence was collected. | Tenant partition review and permission-matrix validation. | Useful control candidates, but not proven at runtime. |
| AUTHZ-MAP-03 | AUTHZ-05 | TH-03 / TH-04 | authorization_flow_map.md; frontend_architecture.md | web/src/app/admin/layout.tsx; web/src/app/admin/users/page.tsx; web/src/app/admin/groups/page.tsx | MISSING-CANDIDATE | The review found admin UI surfaces, but not a dedicated route-by-route authorization audit artifact or separate frontend guard evidence. | No dedicated frontend-backend authorization audit file or route guard proof was identified in this pass. | Frontend/backend authorization alignment review and admin-route audit. | This is a gap in evidence, not proof that authorization is absent. |
