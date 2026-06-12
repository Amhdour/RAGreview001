# PHASE 5 Backend Architecture Map

## 1. Purpose
The backend provides API routing, authentication/authorization hooks, document ingestion/indexing, chat/search orchestration, data access, LLM integration, configuration, and shared utilities.

## 2. Scope
- In scope: `backend/onyx/auth/`, `backend/onyx/chat/`, `backend/onyx/connectors/`, `backend/onyx/db/`, `backend/onyx/document_index/`, `backend/onyx/federated_connectors/`, `backend/onyx/indexing/`, `backend/onyx/llm/`, `backend/onyx/server/`, `backend/onyx/utils/`, and `backend/onyx/configs/`.
- Out of scope: frontend code under `web/`, mobile/desktop clients, test-only behavior, and runtime behavior not represented by backend files.

## 3. Main entry points
- Application composition: `backend/onyx/main.py`.
- API/router modules: `backend/onyx/server/`.
- Authentication and user dependencies: `backend/onyx/auth/users.py`, `backend/onyx/auth/permissions.py`, `backend/onyx/server/auth_check.py`.
- Persistent model definitions and data access helpers: `backend/onyx/db/models.py`, `backend/onyx/db/`.
- Connector framework: `backend/onyx/connectors/interfaces.py`, `backend/onyx/connectors/factory.py`, `backend/onyx/connectors/registry.py`, `backend/onyx/connectors/connector_runner.py`.
- Indexing pipeline: `backend/onyx/indexing/indexing_pipeline.py`, `backend/onyx/indexing/chunker.py`, `backend/onyx/indexing/embedder.py`, `backend/onyx/indexing/vector_db_insertion.py`.
- Document index abstraction/factory: `backend/onyx/document_index/interfaces_new.py`, `backend/onyx/document_index/factory.py`.
- Chat orchestration: `backend/onyx/chat/process_message.py`, `backend/onyx/chat/llm_loop.py`, `backend/onyx/chat/llm_step.py`.
- LLM abstraction/factory: `backend/onyx/llm/interfaces.py`, `backend/onyx/llm/factory.py`, `backend/onyx/llm/multi_llm.py`.
- Configuration: `backend/onyx/configs/app_configs.py`, `backend/onyx/configs/constants.py`, `backend/onyx/configs/agent_configs.py`, `backend/onyx/configs/tool_configs.py`.
- Shared utilities: `backend/onyx/utils/logger.py`, `backend/onyx/utils/telemetry.py`, `backend/onyx/utils/memory_logger.py`.

## 4. Architecture flow
1. `backend/onyx/main.py` constructs the backend application and imports routers from `backend/onyx/server/`.
2. API modules under `backend/onyx/server/` depend on auth helpers in `backend/onyx/auth/` and database helpers in `backend/onyx/db/`.
3. Connector definitions under `backend/onyx/connectors/` provide source-specific document access and shared connector models.
4. Indexing modules under `backend/onyx/indexing/` prepare documents, chunk content, embed chunks, and call vector database insertion helpers.
5. Document index modules under `backend/onyx/document_index/` define the search/index abstraction and the default index factory.
6. Search/chat APIs under `backend/onyx/server/features/search/` and `backend/onyx/server/query_and_chat/` connect request handling to document index, chat, tool, and LLM modules.
7. LLM modules under `backend/onyx/llm/` provide provider/model abstractions used by chat, search, and indexing features.
8. Utility and configuration modules provide cross-cutting logging, telemetry, environment configuration, constants, and runtime helpers.

## 5. Supporting evidence
- `backend/onyx/main.py` — imports FastAPI, auth helpers, and many server routers.
- `backend/onyx/server/` — API route modules grouped by feature area.
- `backend/onyx/auth/users.py` — user/auth backend dependencies, cookie/JWT strategy imports, current-user dependencies, and user helpers.
- `backend/onyx/auth/permissions.py` — permission expansion and FastAPI dependency factory.
- `backend/onyx/db/models.py` — SQLAlchemy models for users, connectors, documents, chat, tools, MCP, build sessions, and related entities.
- `backend/onyx/connectors/interfaces.py` — connector interface definitions.
- `backend/onyx/indexing/indexing_pipeline.py` — indexing pipeline imports for connectors, DB document operations, chunking, embedding, LLM contextual RAG, and document index insertion.
- `backend/onyx/document_index/interfaces_new.py` — document index interface.
- `backend/onyx/llm/interfaces.py` — LLM interface definitions.
- `backend/onyx/chat/process_message.py` — chat message processing entry point.
- `backend/onyx/configs/app_configs.py` — environment-backed application configuration.
- `backend/onyx/utils/logger.py` and `backend/onyx/utils/telemetry.py` — backend logging and telemetry utilities.

## 6. Dependencies
- Internal dependencies: `backend/onyx/server/` depends on auth, DB, chat, connector, indexing, document-index, LLM, tool, and utility modules.
- External services/infrastructure supported by files: relational database through SQLAlchemy models and engine helpers in `backend/onyx/db/`; vector/search backend through `backend/onyx/document_index/`; LLM providers through `backend/onyx/llm/`; cache/Redis-related modules under `backend/onyx/cache/` and `backend/onyx/redis/`.

## 7. Gaps / unknowns
- Exact production service counts and deployment scaling are not established by backend source files alone.
- Runtime activation of optional Enterprise Edition implementations is only mapped where import paths or EE files exist; actual enabled state is deployment-specific and not claimed here.

## 8. Client-ready summary
The backend is organized as a modular Python API service. The central application file wires together route modules. Separate backend packages handle authentication, permissions, database access, connectors, document indexing, search/chat orchestration, LLM providers, configuration, logging, and telemetry.

## Support table
| Claim | Evidence file paths | Support status | Notes |
|---|---|---:|---|
| The backend has a central FastAPI composition file. | `backend/onyx/main.py` | Supported | The file imports FastAPI and router modules. |
| Backend API routes are grouped under the server package. | `backend/onyx/server/` | Supported | The directory contains feature, manage, auth, documents, query/chat, metrics, security, PAT, and federated route modules. |
| Authentication and authorization helpers are separate backend concerns. | `backend/onyx/auth/users.py`, `backend/onyx/auth/permissions.py`, `backend/onyx/server/auth_check.py` | Supported | Auth user dependencies, permission dependencies, and route auth checking are separated. |
| Data persistence is represented by SQLAlchemy models and DB helper modules. | `backend/onyx/db/models.py`, `backend/onyx/db/` | Supported | The models file declares persistent entities; helper files are grouped by domain. |
| RAG ingestion/indexing is represented by connector, indexing, and document-index modules. | `backend/onyx/connectors/`, `backend/onyx/indexing/`, `backend/onyx/document_index/` | Supported | These directories contain connector interfaces, indexing pipeline, chunker/embedder, and document index abstractions. |
| Chat/search generation uses backend chat and LLM modules. | `backend/onyx/chat/`, `backend/onyx/llm/`, `backend/onyx/server/query_and_chat/`, `backend/onyx/server/features/search/api.py` | Supported | Chat, LLM, query/chat routes, and search route files are present. |
| Production scaling behavior is known from backend source files. | No repository evidence identified. | Unsupported | Deployment-specific runtime scaling is not proven by these source files. |

## Missing or unsupported items
- Production scaling, runtime pod counts, and service ownership are unsupported by backend source files alone.
- Optional Enterprise Edition runtime activation is not claimed without deployment configuration evidence.
