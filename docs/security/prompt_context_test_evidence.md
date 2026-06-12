> This is the client-facing mirror of the PHASE 9 evidence file. The canonical evidence copy remains under rag-security-readiness-review/02_evidence/phase_9/.

# PHASE 9 Prompt/Context Test/Evidence Review

## Review phase
PHASE 9 — Map controls to existing tests and evidence

## Category
Prompt/Context

## PHASE 8 linkage
rag-security-readiness-review/02_evidence/phase_8/prompt_risk_to_code.md

## Related PHASE 7 risks
PI-01, PI-02

## Related PHASE 6 threats
TH-01, TH-07, TH-10, TH-11

| Mapping ID | Related PHASE 8 control candidate | Related PHASE 7 risk | Related PHASE 6 threat | Candidate control file/path | Existing test/evidence file/path | Test/evidence label | What the test/evidence appears to cover | Missing evidence | Later validation method | Notes |
|---|---|---|---|---|---|---|---|---|---|---|
| PROMPT-MAP-1 | Prompt/Context Risk to Code | PI-01, PI-02 | TH-01, TH-07, TH-10, TH-11 | backend/onyx/chat/; rag-security-readiness-review/02_evidence/phase_8/prompt_risk_to_code.md | backend/tests/unit/onyx/chat/test_citation_processor.py | UNVERIFIED-COVERAGE | Citation-processing logic is related to prompt/context assembly, but it does not prove prompt-injection resistance. | No adversarial prompt assertion or runtime chat session was collected. | Prompt-injection or context-safety integration test. | The file exists, but the exact control remains unproven. |
| PROMPT-MAP-2 | Prompt/Context Risk to Code | PI-01, PI-02 | TH-01, TH-07, TH-10, TH-11 | backend/onyx/chat/test_citation_utils.py; docs/security/prompt_risk_to_code.md | docs/security/prompt_risk_to_code.md | EVIDENCE-FILE-FOUND | PHASE 8 mapping evidence exists for prompt/context control candidates. | No execution output or adversarial prompt evidence was collected. | Later runtime validation of prompt and context handling. | Evidence is mapping-oriented rather than runtime-oriented. |

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
