> This is the client-facing mirror of the PHASE 9 evidence file. The canonical evidence copy remains under rag-security-readiness-review/02_evidence/phase_9/.

# PHASE 9 Connector Test/Evidence Review

## Review phase
PHASE 9 — Map controls to existing tests and evidence

## Category
Connector

## PHASE 8 linkage
rag-security-readiness-review/02_evidence/phase_8/connector_risk_to_code.md

## Related PHASE 7 risks
CONN-01, CONN-02

## Related PHASE 6 threats
TH-02, TH-05, TH-06, TH-07, TH-14

| Mapping ID | Related PHASE 8 control candidate | Related PHASE 7 risk | Related PHASE 6 threat | Candidate control file/path | Existing test/evidence file/path | Test/evidence label | What the test/evidence appears to cover | Missing evidence | Later validation method | Notes |
|---|---|---|---|---|---|---|---|---|---|---|
| CONN-MAP-1 | Connector Risk to Code | CONN-01, CONN-02 | TH-02, TH-05, TH-06, TH-07, TH-14 | backend/onyx/auth/oauth_token_manager.py; rag-security-readiness-review/02_evidence/phase_8/connector_risk_to_code.md | backend/tests/external_dependency_unit/tools/test_oauth_token_manager.py | TEST-FILE-FOUND | OAuth token-management behavior appears relevant to connector credential handling and refresh logic. | No execution record was collected. | External dependency unit test around connector token refresh. | Discovered test coverage is not execution evidence. |
| CONN-MAP-2 | Connector Risk to Code | CONN-01, CONN-02 | TH-02, TH-05, TH-06, TH-07, TH-14 | backend/onyx/auth/oauth_refresher.py; docs/security/connector_risk_to_code.md | docs/security/connector_risk_to_code.md | EVIDENCE-FILE-FOUND | Source mapping evidence exists for connector-related OAuth refresh and credential flows. | No connector sync execution or live identity-provider check was collected. | Later integration validation against connector sync and token refresh. | Runtime connector behavior remains unverified. |

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
