# PHASE 9 Retrieval ACL Test/Evidence Review

## Review phase
PHASE 9 — Map controls to existing tests and evidence

## Category
Retrieval ACL

## PHASE 8 linkage
rag-security-readiness-review/02_evidence/phase_8/retrieval_acl_risk_to_code.md

## Related PHASE 7 risks
ACL-01, ACL-02

## Related PHASE 6 threats
TH-01, TH-02, TH-03, TH-05, TH-06, TH-08, TH-09

| Mapping ID | Related PHASE 8 control candidate | Related PHASE 7 risk | Related PHASE 6 threat | Candidate control file/path | Existing test/evidence file/path | Test/evidence label | What the test/evidence appears to cover | Missing evidence | Later validation method | Notes |
|---|---|---|---|---|---|---|---|---|---|---|
| ACL-MAP-1 | Retrieval ACL Risk to Code | ACL-01, ACL-02 | TH-01, TH-02, TH-03, TH-05, TH-06, TH-08, TH-09 | backend/tests/integration/multitenant_tests/syncing/test_search_permissions.py | backend/tests/integration/multitenant_tests/syncing/test_search_permissions.py | TEST-FILE-FOUND | Search-permission synchronization across tenants appears relevant to ACL-style retrieval checks. | No execution record was collected. | Integration retrieval ACL test with tenant-separated search results. | A relevant test exists, but execution is unverified. |
| ACL-MAP-2 | Retrieval ACL Risk to Code | ACL-01, ACL-02 | TH-01, TH-02, TH-03, TH-05, TH-06, TH-08, TH-09 | backend/onyx/access/; rag-security-readiness-review/02_evidence/phase_8/retrieval_acl_risk_to_code.md | backend/tests/unit/onyx/access/test_user_file_access.py | UNVERIFIED-COVERAGE | User-file access logic is related to access control, but the file name does not prove search-time ACL enforcement. | No assertion proves retrieval filtering at search time. | Dedicated ACL retrieval integration validation. | Coverage is plausible but not proven. |

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
