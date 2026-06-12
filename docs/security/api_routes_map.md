> This is the client-facing mirror of the PHASE 5 evidence file. The canonical evidence copy remains under rag-security-readiness-review/02_evidence/phase_5/.

# PHASE 5 API Routes Map

## 1. Purpose
This map identifies the backend API route architecture and the frontend proxy routes that expose backend and MCP API paths to the web application.

## 2. Scope
- In scope: `backend/onyx/server/**/api.py`, `backend/onyx/server/manage/**`, `backend/onyx/server/features/**`, `backend/onyx/server/documents/**`, `backend/onyx/server/query_and_chat/**`, `backend/onyx/server/auth/**`, `backend/onyx/server/security/**`, `backend/onyx/server/metrics/**`, `backend/onyx/server/pat/**`, `backend/onyx/server/federated/**`, `backend/onyx/main.py`, `web/src/app/api/[...path]/route.ts`, and `web/src/app/mcp/[[...path]]/route.ts`.
- Out of scope: route behavior not visible in code, unregistered routes not imported by `backend/onyx/main.py`, and external gateway rules not present in repository files.

## 3. Main entry points
- Router registration: `backend/onyx/main.py`.
- Auth/captcha routes: `backend/onyx/server/auth/captcha_api.py`.
- Document/admin connector routes: `backend/onyx/server/documents/connector.py`, `backend/onyx/server/documents/credential.py`, `backend/onyx/server/documents/cc_pair.py`, `backend/onyx/server/documents/document.py`, `backend/onyx/server/documents/standard_oauth.py`, `backend/onyx/server/documents/targeted_reindex.py`.
- Feature routes: `backend/onyx/server/features/search/api.py`, `backend/onyx/server/features/persona/api.py`, `backend/onyx/server/features/tool/api.py`, `backend/onyx/server/features/mcp/api.py`, `backend/onyx/server/features/build/api/api.py`, and peer files under `backend/onyx/server/features/`.
- Management routes: files under `backend/onyx/server/manage/`, including users, LLM, embedding, web search, voice, image generation, Slack/Discord bot, and code interpreter routes.
- Query/chat routes: `backend/onyx/server/query_and_chat/chat_backend.py`, `backend/onyx/server/query_and_chat/query_backend.py`.
- Security/settings/PAT routes: `backend/onyx/server/security/api.py`, `backend/onyx/server/settings/api.py`, `backend/onyx/server/pat/api.py`.
- Federated routes: `backend/onyx/server/federated/api.py`.
- Metrics endpoint support: `backend/onyx/server/metrics/metrics_server.py`, `backend/onyx/server/metrics/prometheus_setup.py`, and other files in `backend/onyx/server/metrics/`.
- Frontend proxy handlers: `web/src/app/api/[...path]/route.ts`, `web/src/app/mcp/[[...path]]/route.ts`.

## 4. Architecture flow
1. `backend/onyx/main.py` imports route modules and registers routers into the FastAPI application.
2. Route modules define `APIRouter` instances and request handlers grouped by domain: documents, features, management, query/chat, auth, security, PAT, federated, and metrics.
3. Authentication/authorization dependencies are applied inside route modules through dependencies from `backend/onyx/auth/users.py`, `backend/onyx/auth/permissions.py`, and related server utility files.
4. Frontend backend requests can pass through the catch-all route handler in `web/src/app/api/[...path]/route.ts`.
5. Frontend MCP requests have a separate catch-all route handler in `web/src/app/mcp/[[...path]]/route.ts`.

## 5. Supporting evidence
- `backend/onyx/main.py` — imports and includes backend routers.
- `backend/onyx/server/features/search/api.py` — search API route definition.
- `backend/onyx/server/query_and_chat/chat_backend.py` — chat session and chat-message API route definitions.
- `backend/onyx/server/query_and_chat/query_backend.py` — query/search API route definitions.
- `backend/onyx/server/documents/connector.py`, `backend/onyx/server/documents/credential.py`, `backend/onyx/server/documents/cc_pair.py` — connector, credential, and connector-credential-pair APIs.
- `backend/onyx/server/features/mcp/api.py`, `backend/onyx/server/features/tool/api.py` — MCP and tool APIs.
- `backend/onyx/server/manage/users.py`, `backend/onyx/server/manage/llm/api.py`, `backend/onyx/server/manage/embedding/api.py` — management APIs.
- `backend/onyx/server/security/api.py`, `backend/onyx/server/pat/api.py`, `backend/onyx/server/federated/api.py` — security, personal access token, and federated APIs.
- `backend/onyx/server/metrics/` — metrics endpoint and metric registration modules.
- `web/src/app/api/[...path]/route.ts`, `web/src/app/mcp/[[...path]]/route.ts` — frontend route handlers for API and MCP paths.

## 6. Dependencies
- Internal dependencies: API route handlers depend on auth, permission, DB, LLM, search, document index, connector, tool, and feature service modules.
- External dependencies supported by files: API routes rely on database/session helpers in `backend/onyx/db/`; search routes rely on document index modules under `backend/onyx/document_index/`; LLM-related routes rely on `backend/onyx/llm/`.

## 7. Gaps / unknowns
- This map identifies route modules and route groups; it does not claim every URL is publicly reachable, because reachability depends on router prefixes, auth dependencies, deployment configuration, and frontend proxy behavior.
- External gateway, load balancer, and ingress behavior is out of scope unless present in deployment files.

## 8. Client-ready summary
The backend API is organized into domain-specific route modules. The main backend application imports those modules and registers them. The frontend includes a general API proxy route plus a separate MCP route, which keeps normal application API traffic and MCP traffic distinct in the frontend source tree.

## Support table
| Claim | Evidence file paths | Support status | Notes |
|---|---|---:|---|
| Router registration is centralized in the backend application file. | `backend/onyx/main.py` | Supported | The file imports routers from many server modules. |
| Document and connector APIs are grouped under the documents server package. | `backend/onyx/server/documents/connector.py`, `backend/onyx/server/documents/credential.py`, `backend/onyx/server/documents/cc_pair.py`, `backend/onyx/server/documents/document.py` | Supported | These files define document/connector route handlers. |
| Search and chat APIs are separate backend route groups. | `backend/onyx/server/features/search/api.py`, `backend/onyx/server/query_and_chat/chat_backend.py`, `backend/onyx/server/query_and_chat/query_backend.py` | Supported | Search and query/chat route files are separate. |
| Management APIs are grouped under `backend/onyx/server/manage/`. | `backend/onyx/server/manage/users.py`, `backend/onyx/server/manage/llm/api.py`, `backend/onyx/server/manage/embedding/api.py` | Supported | The manage directory contains admin/management route modules. |
| MCP and tool APIs have backend feature route modules. | `backend/onyx/server/features/mcp/api.py`, `backend/onyx/server/features/tool/api.py` | Supported | Both feature route files exist. |
| Frontend API and MCP route handlers are separate. | `web/src/app/api/[...path]/route.ts`, `web/src/app/mcp/[[...path]]/route.ts` | Supported | Separate route handlers exist. |
| Every URL is publicly reachable. | No repository evidence identified. | Unsupported | Reachability depends on auth, registration, proxy, and deployment configuration. |

## Missing or unsupported items
- Public reachability of every route is unsupported without combining router prefixes, auth dependencies, and deployment gateway rules in a deeper route audit.
