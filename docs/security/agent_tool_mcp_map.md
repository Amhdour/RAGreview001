> This is the client-facing mirror of the PHASE 5 evidence file. The canonical evidence copy remains under rag-security-readiness-review/02_evidence/phase_5/.

# PHASE 5 Agent / Tool / MCP Map

## 1. Purpose
This map identifies repository evidence for agents/personas, tools/actions, MCP servers/connections, and frontend surfaces that expose those capabilities.

## 2. Scope
- In scope: `backend/onyx/server/features/mcp/`, `backend/onyx/server/features/tool/`, `backend/onyx/server/features/persona/`, `backend/onyx/configs/agent_configs.py`, `backend/onyx/configs/tool_configs.py`, `backend/onyx/tools/`, `backend/onyx/mcp_server/`, `backend/onyx/mcp_server_main.py`, `backend/onyx/db/mcp.py`, `backend/onyx/db/tools.py`, `backend/onyx/db/persona.py`, `web/src/sections/actions/`, `web/src/lib/tools/`, `web/src/app/admin/actions/`, `web/src/app/admin/agents/`, and `web/src/app/mcp/[[...path]]/route.ts`.
- Out of scope: live MCP server credentials, live tool executions, external MCP server behavior, and agent outcome quality.

## 3. Main entry points
- MCP backend feature API: `backend/onyx/server/features/mcp/api.py`, `backend/onyx/server/features/mcp/models.py`.
- MCP server support: `backend/onyx/mcp_server/api.py`, `backend/onyx/mcp_server/auth.py`, `backend/onyx/mcp_server/utils.py`, `backend/onyx/mcp_server_main.py`.
- Tool backend feature API: `backend/onyx/server/features/tool/api.py`, `backend/onyx/server/features/tool/models.py`, `backend/onyx/server/features/tool/tool_visibility.py`.
- Agent/persona backend API: `backend/onyx/server/features/persona/api.py`, `backend/onyx/server/features/persona/models.py`.
- Tool implementations/registration evidence: `backend/onyx/tools/`, `backend/onyx/configs/tool_configs.py`.
- Agent configuration evidence: `backend/onyx/configs/agent_configs.py`.
- Persistent entities/helpers: `backend/onyx/db/models.py`, `backend/onyx/db/mcp.py`, `backend/onyx/db/tools.py`, `backend/onyx/db/persona.py`.
- Frontend MCP/tool services: `web/src/lib/tools/mcpService.ts`, `web/src/lib/tools/openApiService.ts`, `web/src/lib/tools/fetchTools.ts`, `web/src/lib/tools/mcpUtils.tsx`.
- Frontend UI surfaces: `web/src/app/admin/actions/page.tsx`, `web/src/app/admin/agents/page.tsx`, `web/src/sections/actions/`, `web/src/app/mcp/[[...path]]/route.ts`.

## 4. Architecture flow
1. Agent/persona APIs are defined under `backend/onyx/server/features/persona/` and backed by persona DB helper/model files.
2. Tool APIs are defined under `backend/onyx/server/features/tool/`, with tool implementations and configuration under `backend/onyx/tools/` and `backend/onyx/configs/tool_configs.py`.
3. MCP APIs are defined under `backend/onyx/server/features/mcp/`, with MCP server support under `backend/onyx/mcp_server/` and persistent MCP models/helpers under `backend/onyx/db/models.py` and `backend/onyx/db/mcp.py`.
4. Frontend admin pages and service helpers under `web/src/app/admin/actions/`, `web/src/app/admin/agents/`, `web/src/lib/tools/`, and `web/src/sections/actions/` provide UI/service plumbing for agents, actions/tools, and MCP.
5. `web/src/app/mcp/[[...path]]/route.ts` provides a frontend MCP route handler separate from the general API route.

## 5. Supporting evidence
- `backend/onyx/server/features/mcp/api.py`, `backend/onyx/server/features/mcp/models.py` — MCP backend feature API and models.
- `backend/onyx/mcp_server/api.py`, `backend/onyx/mcp_server/auth.py`, `backend/onyx/mcp_server/utils.py`, `backend/onyx/mcp_server_main.py` — MCP server support files.
- `backend/onyx/server/features/tool/api.py`, `backend/onyx/server/features/tool/models.py`, `backend/onyx/server/features/tool/tool_visibility.py` — tool API and visibility files.
- `backend/onyx/server/features/persona/api.py`, `backend/onyx/server/features/persona/models.py` — agent/persona API files.
- `backend/onyx/configs/agent_configs.py`, `backend/onyx/configs/tool_configs.py` — agent/tool configuration evidence.
- `backend/onyx/tools/` — tool implementation package.
- `backend/onyx/db/models.py`, `backend/onyx/db/mcp.py`, `backend/onyx/db/tools.py`, `backend/onyx/db/persona.py` — persistence helpers and entity definitions for these domains.
- `web/src/lib/tools/mcpService.ts`, `web/src/lib/tools/openApiService.ts`, `web/src/lib/tools/fetchTools.ts` — frontend service helpers for tool/MCP actions.
- `web/src/app/admin/actions/page.tsx`, `web/src/app/admin/agents/page.tsx`, `web/src/sections/actions/` — frontend UI surfaces.

## 6. Dependencies
- Internal dependencies: persona/agent routes depend on DB persona helpers, tool routes depend on DB tool helpers and tool implementations, MCP routes depend on DB MCP helpers and MCP server support files.
- External dependencies supported by files: MCP protocol/server integration is represented by the MCP server package and MCP route files; external OpenAPI/custom tool behavior is represented by frontend `openApiService` and backend tool feature files.

## 7. Gaps / unknowns
- Live MCP server connections, enabled tools, per-user credentials, and execution results are runtime data and are not known from repository files.
- Whether a given agent can use a given tool in production requires live configuration and permission review.

## 8. Client-ready summary
Agents/personas, tools/actions, and MCP are implemented as separate but connected areas. The backend has APIs and database helpers for each, and the frontend has admin pages and service helpers that surface them. MCP also has a dedicated frontend route handler and backend MCP server package.

## Support table
| Claim | Evidence file paths | Support status | Notes |
|---|---|---:|---|
| Agent/persona APIs are a backend feature area. | `backend/onyx/server/features/persona/api.py`, `backend/onyx/server/features/persona/models.py` | Supported | Persona feature API/model files exist. |
| Tool/action APIs are a backend feature area. | `backend/onyx/server/features/tool/api.py`, `backend/onyx/server/features/tool/models.py`, `backend/onyx/tools/` | Supported | Tool route/model package and implementations exist. |
| MCP has backend feature APIs and MCP server support files. | `backend/onyx/server/features/mcp/api.py`, `backend/onyx/mcp_server/api.py`, `backend/onyx/mcp_server_main.py` | Supported | MCP feature and server files exist. |
| Agent/tool configuration files exist. | `backend/onyx/configs/agent_configs.py`, `backend/onyx/configs/tool_configs.py` | Supported | Dedicated config files exist. |
| Frontend exposes admin/service plumbing for agents, actions, tools, and MCP. | `web/src/app/admin/actions/page.tsx`, `web/src/app/admin/agents/page.tsx`, `web/src/lib/tools/mcpService.ts`, `web/src/lib/tools/openApiService.ts`, `web/src/sections/actions/` | Supported | UI and service files exist. |
| Live MCP/tool enablement and execution results are known. | No repository evidence identified. | Unsupported | Runtime configuration and execution logs are not present. |

## Missing or unsupported items
- Live MCP server state, enabled tool inventory, per-user credentials, and production agent-tool access are unsupported without runtime configuration/data.
