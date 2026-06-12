# PHASE 5 Architecture Mapping Report

## Executive summary
This report consolidates the PHASE 5 architecture maps into a source-only evidence package. The support tables contain 74 claims: 62 supported and 12 unsupported. The package is complete with limitations and does not claim runtime validation, security control verification, CI/test success, or production readiness. Raw file-search outputs have been added for the architecture evidence categories covered by this phase.

## Architecture scope
- Canonical evidence source: `rag-security-readiness-review/02_evidence/phase_5/`
- Raw evidence output directory: `rag-security-readiness-review/02_evidence/phase_5/raw_outputs/`
- Raw evidence command log: `rag-security-readiness-review/02_evidence/commands/phase_5_raw_architecture_evidence_commands.md`
- Mirror location: `docs/security/`
- Architecture areas covered: backend architecture, frontend architecture, API routes, authentication flow, authorization flow, data model, RAG pipeline, agent/tool/MCP, logging/telemetry, and deployment.
- Out of scope: runtime observation, live service health, live database state, dynamic call graphs, and deployed configuration validation.

## Backend summary
- The backend maps show a FastAPI-centered application structure, domain-specific route modules, DB helpers and models, and separate support packages for retrieval, agents, tools, MCP, logging, telemetry, and deployment-related code paths.
- The maps are source-based; they do not confirm live behavior or environment wiring.

## Frontend summary
- The frontend maps show a Next.js app tree, route handlers, admin surfaces, and client-side plumbing for auth, API routing, and MCP/tool surfaces.
- The maps do not validate rendering, build output, or client runtime behavior.

## API route summary
- Route evidence is organized by backend domains such as documents, search, chat, management, security, PAT, federated, MCP, and tools.
- The frontend contains distinct handlers for general API traffic and MCP traffic.

## Auth flow summary
- Authentication evidence includes main application wiring, user/session helpers, JWT helpers, API key and PAT helpers, OAuth/OIDC/SAML files, and frontend auth screens.
- The maps identify source-level auth surfaces only; they do not verify live authentication configuration.

## Authorization flow summary
- Authorization evidence includes permission enums, permission-dependency helpers, persisted user/group/grant models, token-scope handling, tenant context utilities, and frontend admin-route/UI gating references.
- The maps do not establish current effective permissions for any live user or tenant.

## Data model summary
- Data model evidence includes SQLAlchemy models, enums, helper modules, and migration directories for both standard and tenant-aware schema management.
- The maps do not introspect the runtime database schema or contents.

## RAG pipeline summary
- The RAG maps show a multi-stage flow: connectors, ingestion/admin routes, indexing, chunking, embedding, vector insertion, document-index abstraction, retrieval/search, and chat/answer generation.
- The maps do not measure retrieval quality, corpus size, or production indexing health.

## Agent/tool/MCP summary
- The agent/tool/MCP maps show distinct backend APIs, server support files, config files, persistence helpers, frontend service helpers, and admin UI surfaces.
- The maps do not reveal live tool enablement, server credentials, or execution results.

## Logging/telemetry summary
- The observability maps show logger utilities, telemetry helpers, memory logging, metrics server code, tracing setup, and frontend instrumentation entry points.
- The maps do not confirm alerting, retention, or live telemetry delivery.

## Deployment summary
- Deployment evidence includes backend and frontend Dockerfiles, compose manifests, nginx templates, Helm/Kubernetes support, AWS ECS/Fargate files, and build-sandbox runtime code.
- The maps do not confirm which deployment target is currently active.

## Raw evidence outputs
The following raw file-search outputs were added under `rag-security-readiness-review/02_evidence/phase_5/raw_outputs/`:

- Backend architecture file search: `backend_architecture_file_search.txt`
- Frontend architecture file search: `frontend_architecture_file_search.txt`
- API route file search: `api_route_file_search.txt`
- Auth file search: `auth_file_search.txt`
- Authorization file search: `authorization_file_search.txt`
- Data model file search: `data_model_file_search.txt`
- RAG pipeline file search: `rag_pipeline_file_search.txt`
- Agent/tool/MCP file search: `agent_tool_mcp_file_search.txt`
- Logging/telemetry file search: `logging_telemetry_file_search.txt`
- Deployment file search: `deployment_file_search.txt`

These outputs are supporting file/path inventories, not runtime validation artifacts.

## Claim support method
- Claims were extracted from the support tables in the existing PHASE 5 architecture maps.
- Support was assessed from source-file and path inspection only.
- No runtime execution, test execution, or live service observation was used to elevate any claim.
- Raw architecture outputs were generated with read-only `rg --files` path searches and recorded in the PHASE 5 raw architecture evidence command log.

## Missing evidence
- Dynamic call graphs.
- Live service observations.
- Live database schema/runtime state.
- Deployed configuration and environment variables.
- CI/test results.
- Production validation.

## Limitations
- Source-only limitation.
- Current-checkout limitation.
- Unavailable original source limitation.
- Unavailable working-copy limitation.
- No runtime validation.
- No CI/test validation.
- No production validation.
- File/path search limitation.
- Raw search pattern limitation; path searches may include false positives and may miss relevant files without matching names.
- Inference limitation.
- Missing dynamic call graph limitation.
- Missing running service limitation.
- Missing database runtime schema limitation.
- Missing deployed config limitation.

## Non-claims
- This report does not claim that security controls are verified.
- This report does not claim CI or tests passed.
- This report does not claim production readiness.
- This report does not claim route reachability, live permissions, or operational health.

## PHASE 5 status
COMPLETE WITH LIMITATIONS

## Exact next phase
PHASE 6 — Build threat model
