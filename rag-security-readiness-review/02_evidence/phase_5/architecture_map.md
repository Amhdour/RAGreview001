# PHASE 5 Architecture Map — Master Index

## 1. Purpose
This master map identifies the repository-backed architecture areas reviewed in PHASE 5 and points client reviewers to the detailed maps.

## 2. Scope
- In scope: repository evidence under `backend/onyx/`, `backend/ee/onyx/`, `backend/alembic/`, `web/src/`, `deployment/`, Docker-related files, and PHASE 5 deliverables under `rag-security-readiness-review/02_evidence/phase_5/`.
- Out of scope: runtime claims not proven by files, source areas not requested for PHASE 5, external systems not represented by repository files, and production ownership claims.

## 3. Main entry points
- Backend application entry point: `backend/onyx/main.py`.
- Enterprise backend entry point: `backend/ee/onyx/main.py`.
- Model server entry point: `backend/model_server/main.py`.
- Frontend app router root: `web/src/app/`.
- Frontend API proxy route: `web/src/app/api/[...path]/route.ts`.
- Frontend MCP proxy route: `web/src/app/mcp/[[...path]]/route.ts`.
- Deployment directory: `deployment/`.

## 4. Architecture flow
1. Backend API architecture is anchored by `backend/onyx/main.py`, which imports and registers routers from `backend/onyx/server/`.
2. Frontend architecture is anchored by `web/src/app/`, with server/client instrumentation in `web/src/instrumentation.ts` and `web/src/instrumentation-client.ts`.
3. API traffic from the frontend can be proxied through `web/src/app/api/[...path]/route.ts`; MCP traffic has a separate route in `web/src/app/mcp/[[...path]]/route.ts`.
4. Persistent data models are defined in `backend/onyx/db/models.py`, with migrations under `backend/alembic/` and Enterprise Edition database helpers under `backend/ee/onyx/db/`.
5. RAG-related ingestion and search paths are represented by connector, indexing, document-index, search, chat, and LLM modules under `backend/onyx/`.
6. Deployment evidence is represented by Dockerfiles, compose files, Helm files, nginx templates, and sandbox runtime files.

## 5. Supporting evidence
- `backend/onyx/main.py` — backend FastAPI application composition and router registration.
- `backend/ee/onyx/main.py` — Enterprise Edition backend entry point.
- `backend/model_server/main.py` — model server entry point.
- `web/src/app/` — Next.js App Router pages, layouts, API routes, and feature screens.
- `web/src/app/api/[...path]/route.ts` — frontend API proxy route.
- `web/src/app/mcp/[[...path]]/route.ts` — frontend MCP proxy route.
- `backend/onyx/db/models.py` — SQLAlchemy model declarations.
- `backend/alembic/` — database migration directory.
- `deployment/` — deployment manifests, compose files, Helm files, and nginx templates.

## 6. Dependencies
- Internal dependencies: backend server modules depend on auth, db, document-index, indexing, chat, LLM, connector, and utility modules under `backend/onyx/`.
- Frontend internal dependencies: pages and layouts under `web/src/app/` use shared code under `web/src/lib/`, `web/src/sections/`, `web/src/refresh-pages/`, `web/src/refresh-components/`, and `web/src/layouts/`.
- External infrastructure dependencies supported by files: Postgres/SQLAlchemy (`backend/onyx/db/`, `backend/alembic/`), Redis/cache references (`backend/onyx/cache/`, `backend/onyx/redis/`), Vespa/vector index references (`backend/onyx/document_index/`), Docker/compose (`deployment/docker_compose/`, `backend/Dockerfile`, `web/Dockerfile`), Kubernetes/Helm (`deployment/helm/`).

## 7. Gaps / unknowns
- Runtime topology is not claimed beyond files in `deployment/` and Dockerfiles.
- Service ownership, production SLAs, and cloud account layout are unsupported by repository evidence.
- Actual deployed configuration values are unknown unless present in repository config templates.

## 8. Client-ready summary
The repository separates its architecture into a Python backend, a Next.js frontend, database migrations/models, RAG ingestion and retrieval modules, MCP/tooling modules, telemetry modules, and deployment manifests. The detailed PHASE 5 files below explain each area using only repository file paths as evidence.

## PHASE 5 deliverables
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

## Support table
| Claim | Evidence file paths | Support status | Notes |
|---|---|---:|---|
| Backend composition is centered in a FastAPI application file. | `backend/onyx/main.py` | Supported | The file imports FastAPI and backend routers. |
| Frontend composition is centered in the Next.js app source tree. | `web/src/app/`, `web/src/app/layout.tsx`, `web/src/app/api/[...path]/route.ts` | Supported | The app tree contains pages, layouts, and route handlers. |
| Persistent data models and migrations are represented in the backend tree. | `backend/onyx/db/models.py`, `backend/alembic/` | Supported | Models and migrations are both present. |
| Deployment wiring is represented in repository deployment files. | `deployment/`, `backend/Dockerfile`, `web/Dockerfile` | Supported | Compose, Helm, nginx, and Docker evidence exists. |
| Production runtime ownership and SLA boundaries are known. | No repository evidence identified. | Unsupported | No ownership/SLA files were reviewed. |

## Missing or unsupported items
- Production ownership, SLAs, and actual deployed cloud account topology are unsupported by repository evidence.
- Runtime behavior is only mapped where repository code/config files provide support.
