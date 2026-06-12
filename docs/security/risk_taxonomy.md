> This is the client-facing mirror of the PHASE 7 evidence file. The canonical evidence copy remains under rag-security-readiness-review/02_evidence/phase_7/.

# PHASE 7 Risk Taxonomy

## Review metadata
- Review phase: PHASE 7 — Create risk taxonomy
- Repository: Amhdour/RAGreview001
- Source input type: GitHub repository workspace
- Date/time: 2026-06-12T10:02:54Z
- Reviewer: Codex
- Prepared by: Codex
- Approved by: NOT AVAILABLE

## Dependencies
- PHASE 2 dependency: PHASE 2 review boundaries, scope, claim boundaries, evidence standards, and testing rules under `rag-security-readiness-review/02_evidence/phase_2/`.
- PHASE 5 dependency: PHASE 5 architecture map and related architecture evidence under `rag-security-readiness-review/02_evidence/phase_5/`.
- PHASE 6 dependency: PHASE 6 threat model and threat register under `rag-security-readiness-review/02_evidence/phase_6/`.

## Risk-taxonomy objective
Organize the PHASE 6 threat model into evidence-linked risk categories that remain faithful to the PHASE 2 boundaries, the PHASE 5 architecture map, and the source-only evidence available in the current checkout.

## Evidence basis
- `rag-security-readiness-review/03_reports/phase_2_review_boundaries_report.md`
- `rag-security-readiness-review/02_evidence/phase_2/scope.md`
- `rag-security-readiness-review/02_evidence/phase_2/claim_boundaries.md`
- `rag-security-readiness-review/02_evidence/phase_2/testing_rules.md`
- `rag-security-readiness-review/03_reports/phase_5_architecture_mapping_report.md`
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
- `rag-security-readiness-review/03_reports/phase_6_threat_model_report.md`
- `rag-security-readiness-review/02_evidence/phase_6/threat_model.md`
- `rag-security-readiness-review/02_evidence/phase_6/protected_assets.md`
- `rag-security-readiness-review/02_evidence/phase_6/actors_and_roles.md`
- `rag-security-readiness-review/02_evidence/phase_6/trust_boundaries.md`
- `rag-security-readiness-review/02_evidence/phase_6/data_flows.md`
- `rag-security-readiness-review/02_evidence/phase_6/abuse_cases.md`
- `rag-security-readiness-review/02_evidence/phase_6/highest_risk_paths.md`
- `rag-security-readiness-review/02_evidence/phase_6/threat_register.md`
- `rag-security-readiness-review/02_evidence/phase_6/threat_to_architecture_map.md`

## Risk evidence labels
- EVIDENCE-LINKED: linked to PHASE 6 threat evidence and PHASE 5 architecture evidence.
- INFERRED: inferred from architecture and threat-model evidence without direct validation.
- UNVERIFIED: relevant to the taxonomy but not directly validated from source-only evidence.

## Risk priority language
- Critical candidate
- High candidate
- Medium candidate
- Low candidate
- Informational
- Unverified

## Category summary table

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

## Cross-category risk themes
- Retrieval, authorization, and retrieval-ACL boundaries repeat across RAG, authz, and prompt-injection categories.
- Connector, ingestion, and indexing issues can propagate into RAG quality, retrieval leakage, and prompt-injection exposure.
- Agent and tool/MCP risks share a common concern: untrusted context can become action, not just text.
- Logging and telemetry can amplify leakage from prompts, documents, and credentials if redaction is weak or unverified.
- Deployment and supply-chain concerns can widen the blast radius of every other category when runtime configuration is unknown.
- Several risks remain inferred or unverified because this phase is source-only and has no runtime evidence.

## Risk-to-threat map link
- `rag-security-readiness-review/02_evidence/phase_7/risk_to_threat_map.md`

## Risk-to-architecture map link
- `rag-security-readiness-review/02_evidence/phase_7/risk_to_architecture_map.md`

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

## Next phase
PHASE 8 — Map controls to risks
