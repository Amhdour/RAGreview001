# PHASE 7 Risk Taxonomy Report

## Executive summary
PHASE 7 created a source-only, evidence-linked risk taxonomy from the PHASE 6 threat model. The taxonomy is organized by the requested ten categories and remains bounded by the PHASE 2 scope, the PHASE 5 architecture evidence, and the current checkout of the repository.

## Evidence basis
- `rag-security-readiness-review/02_evidence/phase_2/scope.md`
- `rag-security-readiness-review/02_evidence/phase_2/claim_boundaries.md`
- `rag-security-readiness-review/02_evidence/phase_2/testing_rules.md`
- `rag-security-readiness-review/02_evidence/phase_5/architecture_map.md`
- `rag-security-readiness-review/02_evidence/phase_5/backend_architecture.md`
- `rag-security-readiness-review/02_evidence/phase_5/frontend_architecture.md`
- `rag-security-readiness-review/02_evidence/phase_5/api_routes_map.md`
- `rag-security-readiness-review/02_evidence/phase_5/auth_flow_map.md`
- `rag-security-readiness-review/02_evidence/phase_5/authorization_flow_map.md`
- `rag-security-readiness-review/02_evidence/phase_5/data_model_map.md`
- `rag-security-readiness-review/02_evidence/phase_5/rag_pipeline_map.md`
- `rag-security-readiness-review/02_evidence/phase_5/agent_tool_mcp_map.md`
- `rag-security-readiness-review/02_evidence/phase_5/logging_telemetry_map.md`
- `rag-security-readiness-review/02_evidence/phase_5/deployment_flow_map.md`
- `rag-security-readiness-review/02_evidence/phase_6/threat_model.md`
- `rag-security-readiness-review/02_evidence/phase_6/threat_register.md`

## Category coverage summary
| Category | Purpose | Related PHASE 6 threats | Related PHASE 5 areas | Highest candidate priority | Evidence status | Notes |
| --- | --- | --- | --- | --- | --- | --- |
| RAG Risks | Organize retrieval, search, answer-generation, and citation risks. | TH-01, TH-02, TH-06, TH-08, TH-09 | rag_pipeline_map.md; api_routes_map.md; authorization_flow_map.md; backend_architecture.md | Critical candidate | Mixed: EVIDENCE-LINKED / INFERRED / UNVERIFIED | The category links search and chat exposure risks to repository-backed retrieval and citation surfaces while preserving the source-only limitation. |
| Agent Risks | Capture risks introduced when LLM-driven or background agent behavior can act on retrieved context or invoke tools. | TH-01, TH-07, TH-11, TH-12 | agent_tool_mcp_map.md; backend_architecture.md; rag_pipeline_map.md | Critical candidate | Mixed: EVIDENCE-LINKED / INFERRED | The category shows how injected content, tool execution, and ambiguous agent state can widen the impact of retrieval or tool misuse. |
| Authentication Risks | Track risks around identity establishment, token use, and federation configuration. | TH-13, TH-14 | auth_flow_map.md | Critical candidate | Mixed: EVIDENCE-LINKED / INFERRED / UNVERIFIED | The category remains source-only and distinguishes confirmed token surfaces from unverified federation and lifecycle behavior. |
| Authorization Risks | Capture access-control failures between authenticated identities and permitted resources or actions. | TH-02, TH-03, TH-04 | api_routes_map.md; authorization_flow_map.md; data_model_map.md | Critical candidate | Mixed: EVIDENCE-LINKED / INFERRED / UNVERIFIED | The category isolates document and admin control failures from broader retrieval or agent issues. |
| Retrieval ACL Risks | Track document-level ACL and indexing risks that can let search or citations surface restricted content. | TH-01, TH-02, TH-03, TH-05, TH-06, TH-08 | rag_pipeline_map.md; authorization_flow_map.md; data_model_map.md; api_routes_map.md | Critical candidate | Mixed: EVIDENCE-LINKED / INFERRED / UNVERIFIED | The category focuses on content that should be hidden but may still be reachable through retrieval or provenance metadata. |
| Prompt-Injection Risks | Describe how malicious content can influence prompts, retrieval, or tool use. | TH-01, TH-07, TH-10, TH-11 | backend_architecture.md; rag_pipeline_map.md; agent_tool_mcp_map.md | Critical candidate | Mixed: EVIDENCE-LINKED / INFERRED | This category records how untrusted content can reshape model behavior even when the underlying source evidence is only static. |
| Connector Risks | Capture risks in source-system authentication, permission scope, and sync behavior. | TH-02, TH-05, TH-06, TH-07 | rag_pipeline_map.md; auth_flow_map.md | Critical candidate | Mixed: EVIDENCE-LINKED / INFERRED | The category keeps connector exposure separate from generic retrieval because it starts at the external source boundary. |
| Tool/MCP Risks | Describe risks around tool registration, MCP exposure, and tool execution control. | TH-07, TH-11 | agent_tool_mcp_map.md; api_routes_map.md | Critical candidate | Mixed: EVIDENCE-LINKED / INFERRED / UNVERIFIED | The category isolates direct tool execution and MCP exposure from broader agent or prompt concerns. |
| Logging/Telemetry Risks | Track how observability systems can leak prompts, documents, or tokens. | TH-01, TH-10, TH-13, TH-15 | logging_telemetry_map.md | Critical candidate | Mixed: EVIDENCE-LINKED / UNVERIFIED | The category shows how prompt and document data can leak from systems intended for visibility, not disclosure. |
| Deployment/Supply-Chain Risks | Capture repository-backed deployment and build-path risks that may expose secrets or runtime misconfiguration. | TH-12, TH-15, TH-16 | deployment_flow_map.md; architecture_map.md | Critical candidate | Mixed: EVIDENCE-LINKED / INFERRED / UNVERIFIED | The category records the deployment and supply-chain surface while preserving the limitation that no live environment was inspected. |

## Risk evidence-label summary
- EVIDENCE-LINKED: 25
- INFERRED: 15
- UNVERIFIED: 10

## Candidate-priority summary
- Critical candidate: 12
- High candidate: 21
- Medium candidate: 13
- Low candidate: 0
- Informational: 4
- Unverified: 0

## PHASE 6 threat coverage
- Covered threats: TH-01, TH-02, TH-03, TH-04, TH-05, TH-06, TH-07, TH-08, TH-09, TH-10, TH-11, TH-12, TH-13, TH-14, TH-15, TH-16
- PHASE 6 classifications remain source-based and are not a statement of exploitability.

## PHASE 5 architecture linkage
- Each category links back to the relevant PHASE 5 architecture files and supporting paths.
- The taxonomy uses architecture files to explain where the risk surface originates, not to verify runtime control effectiveness.

## Missing evidence
- No runtime validation of retrieval, authz, agent behavior, tool execution, or telemetry emission.
- No live connector, database, vector index, or production inspection.
- No exploit validation, CI validation, or application-test validation.

## Limitations
- Source-only evidence.
- Current-checkout limitation.
- Original source and working-copy limitations remain in place.
- Production/live evidence is unavailable.
- Candidate priorities are not final severities.

## Non-claims
- No claim of exploitability.
- No claim of security-control verification.
- No claim of production readiness.
- No claim that any PHASE 6 threat is a confirmed vulnerability.

## PHASE 7 status
- COMPLETE
- COMPLETE WITH LIMITATIONS
- BLOCKED

## Exact next phase
PHASE 8 — Map controls to risks
