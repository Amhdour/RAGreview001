# PHASE 9 Agent/Tool/MCP Test/Evidence Review

## Review phase
PHASE 9 — Map controls to existing tests and evidence

## Category
Agent/Tool/MCP

## PHASE 8 linkage
rag-security-readiness-review/02_evidence/phase_8/agent_tool_mcp_risk_to_code.md

## Related PHASE 7 risks
AGENT-01, AGENT-02

## Related PHASE 6 threats
TH-07, TH-11, TH-12

| Mapping ID | Related PHASE 8 control candidate | Related PHASE 7 risk | Related PHASE 6 threat | Candidate control file/path | Existing test/evidence file/path | Test/evidence label | What the test/evidence appears to cover | Missing evidence | Later validation method | Notes |
|---|---|---|---|---|---|---|---|---|---|---|
| MCP-MAP-1 | Agent/Tool/MCP Risk to Code | AGENT-01, AGENT-02 | TH-07, TH-11, TH-12 | backend/onyx/server/features/mcp/; rag-security-readiness-review/02_evidence/phase_8/agent_tool_mcp_risk_to_code.md | backend/tests/unit/onyx/server/features/mcp/test_per_user_listing_invariants.py | TEST-FILE-FOUND | Per-user listing invariants appear relevant to tool/MCP access-control behavior. | No execution record was collected. | Unit-level MCP permission and listing invariant test. | File existence does not establish executed security behavior. |
| MCP-MAP-2 | Agent/Tool/MCP Risk to Code | AGENT-01, AGENT-02 | TH-07, TH-11, TH-12 | web/tests/e2e/mcp/mcp_oauth_flow.spec.ts; docs/security/agent_tool_mcp_risk_to_code.md | web/tests/e2e/mcp/mcp_oauth_flow.spec.ts | UNVERIFIED-COVERAGE | The E2E spec suggests MCP OAuth coverage, but the spec was not executed. | No Playwright execution or runtime sandbox evidence was collected. | Later Playwright or integration validation for MCP OAuth and tool invocation. | Coverage exists on disk, but execution is absent. |

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
