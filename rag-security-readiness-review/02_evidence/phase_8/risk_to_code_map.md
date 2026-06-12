# PHASE 8 Risk to Code Map

## Review phase
PHASE 8 — Map controls to risks

## Repository
Amhdour/RAGreview001

## Source input type
GitHub repository workspace

## Date/time
2026-06-12T11:20:54Z

## Reviewer
Codex

## Prepared by
Codex

## Approved by
UNCONFIRMED

## PHASE 3 dependency
PHASE 3 baseline inventory evidence was used to anchor the current-checkout file inventory and the security-relevant path index.

## PHASE 5 dependency
PHASE 5 architecture evidence was used to connect code paths to the documented system surface before selecting control candidates.

## PHASE 6 dependency
PHASE 6 threat evidence was used to anchor each code mapping to a threat ID where available.

## PHASE 7 dependency
PHASE 7 risk taxonomy evidence was used to anchor each mapping to a specific risk category and risk ID.

## Objective
Create an evidence-backed risk-to-code/control map that links PHASE 7 risks, PHASE 6 threats, PHASE 5 architecture evidence, PHASE 3 inventory evidence, and current-checkout file paths without claiming control effectiveness.

## Evidence basis
Source-only mapping from the current checkout, backed by PHASE 3 through PHASE 7 review artifacts and file/path searches.

## Mapping labels
- EXISTING-CANDIDATE
- MISSING-CANDIDATE
- UNVERIFIED
- NOT-APPLICABLE

## Category summary table

| Mapping category | Related PHASE 7 category | Related PHASE 6 threats | Main PHASE 5 architecture areas | Candidate code paths found | Existing candidates | Missing candidates | Unverified mappings | Notes |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Authentication Risk to Code | AUTH-01, AUTH-02 | TH-13, TH-14 | auth_flow_map.md; api_routes_map.md; backend_architecture.md; frontend_architecture.md | 14 | 2 | 0 | 1 | Source-only evidence with later validation still required. |
| Authorization Risk to Code | AUTHZ-01, AUTHZ-02 | TH-02, TH-03, TH-04 | api_routes_map.md; authorization_flow_map.md; data_model_map.md; frontend_architecture.md | 9 | 2 | 1 | 0 | Source-only evidence with later validation still required. |
| Retrieval ACL Risk to Code | ACL-01, ACL-02 | TH-01, TH-02, TH-03, TH-05, TH-06, TH-08, TH-09 | rag_pipeline_map.md; authorization_flow_map.md; data_model_map.md; api_routes_map.md | 11 | 2 | 0 | 1 | Source-only evidence with later validation still required. |
| Ingestion Risk to Code | RAG-03, RAG-05 | TH-05, TH-06, TH-07, TH-09 | rag_pipeline_map.md; backend_architecture.md; data_model_map.md; api_routes_map.md | 10 | 2 | 1 | 0 | Source-only evidence with later validation still required. |
| Prompt/Context Risk to Code | PI-01, PI-02 | TH-01, TH-07, TH-10, TH-11 | backend_architecture.md; rag_pipeline_map.md; agent_tool_mcp_map.md | 11 | 2 | 0 | 1 | Source-only evidence with later validation still required. |
| Connector Risk to Code | CONN-01, CONN-02 | TH-02, TH-05, TH-06, TH-07, TH-14 | rag_pipeline_map.md; auth_flow_map.md; backend_architecture.md | 13 | 2 | 1 | 0 | Source-only evidence with later validation still required. |
| Agent/Tool/MCP Risk to Code | AGENT-01, AGENT-02 | TH-07, TH-11, TH-12 | agent_tool_mcp_map.md; api_routes_map.md; backend_architecture.md; rag_pipeline_map.md | 12 | 2 | 0 | 1 | Source-only evidence with later validation still required. |
| Logging/Telemetry Risk to Code | LOG-01, LOG-02 | TH-10, TH-13, TH-15 | logging_telemetry_map.md; backend_architecture.md; deployment_flow_map.md | 11 | 2 | 1 | 0 | Source-only evidence with later validation still required. |
| Deployment/CI Risk to Code | DEP-01, DEP-02 | TH-12, TH-15, TH-16 | deployment_flow_map.md; architecture_map.md | 12 | 2 | 1 | 0 | Source-only evidence with later validation still required. |

## Control candidate summary
27 control candidate rows were recorded across the nine categories, with 18 existing-candidate rows.

## Missing control summary
5 mapping rows were marked MISSING-CANDIDATE, and 6 missing-control follow-up candidates were recorded because expected control evidence was absent or insufficient in this pass.

## Unverified mapping summary
4 rows were marked UNVERIFIED because source-only evidence could not confirm the runtime control effect.

## Risk-to-code coverage summary
- AUTH-01
- AUTH-02
- AUTH-03
- AUTH-04
- AUTH-05
- RAG-01
- RAG-02
- AUTHZ-01
- AUTHZ-02
- AUTHZ-03
- AUTHZ-04
- AUTHZ-05
- ACL-01
- ACL-02
- ACL-03
- ACL-04
- ACL-05
- RAG-03
- RAG-04
- RAG-05
- PI-01
- CONN-04
- CONN-05
- PI-02
- PI-03
- PI-04
- PI-05
- AGENT-02
- CONN-01
- CONN-02
- CONN-03
- AGENT-01
- AGENT-03
- AGENT-04
- TOOL-01
- TOOL-02
- TOOL-03
- TOOL-04
- TOOL-05
- LOG-01
- LOG-02
- LOG-03
- LOG-04
- LOG-05
- DEP-01
- DEP-02
- DEP-03
- DEP-04
- DEP-05
- DEP-06

## Missing evidence
- No runtime validation of any mapped control candidate.
- No CI or application-test validation.
- No live production, connector, database, or observability sink validation.

## Limitations
- Source-only mapping.
- Current-checkout limitation.
- Original source and working-copy limitations remain in place.
- Some mappings are missing or unverified.

## Non-claims
- No claim that any control is effective.
- No claim that any risk is mitigated.
- No claim that missing evidence proves absence of a control.

## Next phase
PHASE 9 — Map controls to existing tests and evidence

