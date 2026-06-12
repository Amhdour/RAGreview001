# Threat to Architecture Map

| Threat ID | Architecture area | PHASE 5 architecture file | Supporting file/path | Evidence status | Related abuse case | Limitation |
| --- | --- | --- | --- | --- | --- | --- |
| TH-01 | Retrieval/search | `rag-security-readiness-review/02_evidence/phase_5/rag_pipeline_map.md` | `backend/onyx/server/features/search/`, `backend/onyx/document_index/` | FILE-SUPPORTED | AC-01 | No runtime query or permission test. |
| TH-02 | Authorization / multi-tenant scoping | `rag-security-readiness-review/02_evidence/phase_5/authorization_flow_map.md` | `backend/onyx/db/models.py`, `backend/onyx/server/` | FILE-SUPPORTED | AC-02; AC-26 | No live tenant state was inspected. |
| TH-03 | API routes | `rag-security-readiness-review/02_evidence/phase_5/api_routes_map.md` | `backend/onyx/server/documents/`, `backend/onyx/server/features/` | FILE-SUPPORTED | AC-03 | Route registration does not prove runtime reachability. |
| TH-04 | Management/API routes | `rag-security-readiness-review/02_evidence/phase_5/api_routes_map.md` | `backend/onyx/server/manage/` | FILE-SUPPORTED | AC-04; AC-25 | No live permission matrix. |
| TH-05 | Connector / credentials | `rag-security-readiness-review/02_evidence/phase_5/rag_pipeline_map.md` | `backend/onyx/connectors/`, `backend/onyx/server/documents/credential.py` | FILE-SUPPORTED | AC-05 | Secret values were not exposed. |
| TH-06 | Ingestion / connector sync | `rag-security-readiness-review/02_evidence/phase_5/rag_pipeline_map.md` | `backend/onyx/indexing/`, `backend/onyx/connectors/` | FILE-SUPPORTED | AC-06; AC-07 | No live sync scope verification. |
| TH-07 | Ingestion / prompt context | `rag-security-readiness-review/02_evidence/phase_5/backend_architecture.md` | `backend/onyx/chat/`, `backend/onyx/llm/` | FILE-SUPPORTED | AC-08; AC-09; AC-10 | No runtime prompt-injection test. |
| TH-08 | Retrieval / citation return | `rag-security-readiness-review/02_evidence/phase_5/rag_pipeline_map.md` | `backend/onyx/server/features/search/`, `backend/onyx/chat/` | INFERRED | AC-11 | Citation integrity was not validated. |
| TH-09 | Indexing / retrieval | `rag-security-readiness-review/02_evidence/phase_5/backend_architecture.md` | `backend/onyx/indexing/`, `backend/onyx/document_index/` | FILE-SUPPORTED | AC-12; AC-13 | No live index poisoning test. |
| TH-10 | Logging / telemetry | `rag-security-readiness-review/02_evidence/phase_5/logging_telemetry_map.md` | `backend/onyx/utils/logger.py`, `backend/onyx/utils/telemetry.py` | FILE-SUPPORTED | AC-14; AC-15; AC-16 | No live observability sink access. |
| TH-11 | Tool / agent / MCP | `rag-security-readiness-review/02_evidence/phase_5/agent_tool_mcp_map.md` | `backend/onyx/server/features/mcp/api.py`, `backend/onyx/server/features/tool/api.py` | FILE-SUPPORTED | AC-17; AC-18; AC-19 | No live tool authorization test. |
| TH-12 | Sandbox / file handling | `rag-security-readiness-review/02_evidence/phase_5/logging_telemetry_map.md` | `backend/onyx/server/features/build/sandbox/` | FILE-SUPPORTED | AC-20; AC-21 | No sandbox execution was observed. |
| TH-13 | Authentication | `rag-security-readiness-review/02_evidence/phase_5/auth_flow_map.md` | `backend/onyx/auth/`, `backend/onyx/server/pat/api.py` | FILE-SUPPORTED | AC-22; AC-23 | No live token lifecycle validation. |
| TH-14 | Authentication / federation | `rag-security-readiness-review/02_evidence/phase_5/auth_flow_map.md` | `backend/onyx/server/saml.py`, `backend/onyx/auth/oauth_token_manager.py` | FILE-SUPPORTED | AC-24 | No live IdP configuration review. |
| TH-15 | Deployment/runtime | `rag-security-readiness-review/02_evidence/phase_5/deployment_flow_map.md` | `deployment/`, `backend/onyx/configs/app_configs.py` | FILE-SUPPORTED | AC-27 | No live deployment inspection. |
| TH-16 | CI/CD / supply-chain | `rag-security-readiness-review/02_evidence/phase_5/deployment_flow_map.md` | `deployment/` | NOT FOUND | AC-28 | No explicit CI/CD workflow evidence. |
