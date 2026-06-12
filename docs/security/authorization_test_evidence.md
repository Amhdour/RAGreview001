> This is the client-facing mirror of the PHASE 9 evidence file. The canonical evidence copy remains under rag-security-readiness-review/02_evidence/phase_9/.

# PHASE 9 Authorization Test/Evidence Review

## Review phase
PHASE 9 — Map controls to existing tests and evidence

## Category
Authorization

## PHASE 8 linkage
rag-security-readiness-review/02_evidence/phase_8/authorization_risk_to_code.md

## Related PHASE 7 risks
AUTHZ-01, AUTHZ-02

## Related PHASE 6 threats
TH-02, TH-03, TH-04

| Mapping ID | Related PHASE 8 control candidate | Related PHASE 7 risk | Related PHASE 6 threat | Candidate control file/path | Existing test/evidence file/path | Test/evidence label | What the test/evidence appears to cover | Missing evidence | Later validation method | Notes |
|---|---|---|---|---|---|---|---|---|---|---|
| AUTHZ-MAP-1 | Authorization Risk to Code | AUTHZ-01, AUTHZ-02 | TH-02, TH-03, TH-04 | backend/onyx/auth/permissions.py; rag-security-readiness-review/02_evidence/phase_8/authorization_risk_to_code.md | backend/tests/unit/onyx/auth/test_permissions.py | TEST-FILE-FOUND | Permission resolution, implied permissions, and auth dependency helpers appear covered. | No execution record was collected. | Targeted unit tests for permission helpers and auth dependencies. | File existence is not proof of enforcement. |
| AUTHZ-MAP-2 | Authorization Risk to Code | AUTHZ-01, AUTHZ-02 | TH-02, TH-03, TH-04 | backend/onyx/server/auth_check.py; docs/security/authorization_risk_to_code.md | docs/security/authorization_risk_to_code.md | EVIDENCE-FILE-FOUND | Source mapping evidence exists for backend auth checks. | No runtime deny/allow evidence was collected. | Integration/API request validation for private and admin routes. | Evidence supports mapping, not effectiveness. |

## Evidence basis
- The category is anchored to PHASE 8 evidence and the PHASE 7/PHASE 6 lineage above.
- File discovery for this pass was limited to the current checkout and the searched test/evidence directories.

## Missing evidence
- No test execution output was collected for the discovered test files.
- No CI run output was collected for the evidence files.
- No runtime validation was performed in this pass.

## Limitations
- Source-only review.
- Current-checkout limitation.
- Original source unavailable.
- Working copy unavailable.
- Existing files do not prove execution or enforcement.

## Non-claims
- No claim of effectiveness.
- No claim of test pass status.
- No claim of CI success.
- No claim of production readiness.
