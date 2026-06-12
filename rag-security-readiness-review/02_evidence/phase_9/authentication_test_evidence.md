# PHASE 9 Authentication Test/Evidence Review

## Review phase
PHASE 9 — Map controls to existing tests and evidence

## Category
Authentication

## PHASE 8 linkage
rag-security-readiness-review/02_evidence/phase_8/auth_risk_to_code.md

## Related PHASE 7 risks
AUTH-01, AUTH-02

## Related PHASE 6 threats
TH-13, TH-14

| Mapping ID | Related PHASE 8 control candidate | Related PHASE 7 risk | Related PHASE 6 threat | Candidate control file/path | Existing test/evidence file/path | Test/evidence label | What the test/evidence appears to cover | Missing evidence | Later validation method | Notes |
|---|---|---|---|---|---|---|---|---|---|---|
| AUTH-MAP-1 | Authentication Risk to Code | AUTH-01, AUTH-02 | TH-13, TH-14 | backend/onyx/auth/users.py; rag-security-readiness-review/02_evidence/phase_8/auth_risk_to_code.md | backend/tests/unit/onyx/auth/test_user_registration.py | TEST-FILE-FOUND | Registration, disposable-email gating, invite logic, and SSO bypass behavior appear to be covered. | No execution record was collected. | Targeted pytest run for auth registration and verification paths. | File exists in the searched tree; execution remains unverified. |
| AUTH-MAP-2 | Authentication Risk to Code | AUTH-01, AUTH-02 | TH-13, TH-14 | web/src/app/auth/login/page.tsx; rag-security-readiness-review/02_evidence/phase_9/authentication_review/auth_tests_review.md | rag-security-readiness-review/02_evidence/phase_9/authentication_review/auth_tests_review.md | EVIDENCE-FILE-FOUND | Focused authentication review and test survey exist. | No runtime validation or CI evidence was collected. | Playwright auth flow validation plus backend auth integration checks. | PHASE 9A evidence only; not full control coverage. |

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
