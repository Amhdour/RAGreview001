> This is the client-facing mirror of the PHASE 8 evidence file. The canonical evidence copy remains under rag-security-readiness-review/02_evidence/phase_8/.

# Agent/Tool/MCP Risk to Code

## Category purpose
Map agent orchestration, tool registries, MCP APIs, and sandbox/approval surfaces that can turn text into actions.

## Related PHASE 7 risks
- AGENT-01
- AGENT-02
- AGENT-03
- AGENT-04
- TOOL-01
- TOOL-02
- TOOL-03
- TOOL-04
- TOOL-05
- PI-04

## Related PHASE 6 threats
- TH-07
- TH-11
- TH-12

## Related PHASE 5 architecture evidence
- rag-security-readiness-review/02_evidence/phase_5/agent_tool_mcp_map.md
- rag-security-readiness-review/02_evidence/phase_5/api_routes_map.md
- rag-security-readiness-review/02_evidence/phase_5/backend_architecture.md
- rag-security-readiness-review/02_evidence/phase_5/rag_pipeline_map.md

## Related PHASE 3 inventory evidence
- rag-security-readiness-review/02_evidence/phase_3/baseline_inventory.md
- rag-security-readiness-review/02_evidence/phase_3/important_files_index.md
- rag-security-readiness-review/02_evidence/phase_3/security_relevant_files.md

## Candidate Onyx file paths
- backend/onyx/server/features/tool/api.py
- backend/onyx/server/features/tool/models.py
- backend/onyx/server/features/tool/tool_visibility.py
- backend/onyx/mcp_server/api.py
- backend/onyx/mcp_server/auth.py
- backend/onyx/mcp_server/tools/search.py
- backend/onyx/mcp_server_main.py
- backend/onyx/hooks/registry.py
- backend/onyx/hooks/executor.py
- backend/onyx/hooks/api_dependencies.py
- backend/onyx/server/features/build/sandbox/util/agent_instructions.py
- backend/onyx/server/features/build/sandbox/tasks/tasks.py

## Existing control candidates
- AGENT-MAP-01: tool API and visibility files appear present.
- AGENT-MAP-02: MCP API, auth, search tools, and hook executor files appear present.

## Missing control candidates
- No runtime approval-flow validation was collected.

## Unverified mappings
- AGENT-MAP-03: sandbox isolation and human-in-the-loop handling remain unverified.

## Later validation methods
- Tool authorization review.
- MCP endpoint exposure validation.
- Approval-flow and sandbox-isolation review.

## Non-claims
- No claim that tool execution is safe.
- No claim that the sandbox or approval model is validated.

## Client-ready summary
The agent/tool/MCP surface has several clear control candidates, but the current pass does not verify whether they actually gate execution safely.

## Mapping table

| Mapping ID | Related risk ID/category | Related PHASE 6 threat ID | Related PHASE 5 architecture evidence | Candidate Onyx file/path | Mapping label | Why this file/path matters | Missing evidence | Later validation method | Notes |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| AGENT-MAP-01 | AGENT-01 / TOOL-01 / TOOL-02 | TH-11 | agent_tool_mcp_map.md; api_routes_map.md; backend_architecture.md | backend/onyx/server/features/tool/api.py; backend/onyx/server/features/tool/models.py; backend/onyx/server/features/tool/tool_visibility.py | EXISTING-CANDIDATE | These tool API and visibility files appear to control registration and exposure of tool actions. | No live authorization or approval-flow validation for tool execution was run. | Tool-authorization and tool-visibility runtime validation. | Candidate control point for tool governance. |
| AGENT-MAP-02 | AGENT-02 / TOOL-03 / TOOL-04 | TH-07 / TH-11 | agent_tool_mcp_map.md; api_routes_map.md; backend_architecture.md | backend/onyx/mcp_server/api.py; backend/onyx/mcp_server/auth.py; backend/onyx/mcp_server/tools/search.py; backend/onyx/mcp_server_main.py; backend/onyx/hooks/registry.py; backend/onyx/hooks/executor.py | EXISTING-CANDIDATE | These files suggest the MCP and hook execution surfaces that can expose or run tools. | No live MCP endpoint exposure review or approval gate validation was performed. | MCP endpoint and executor review. | Potential enforcement point for safe tool execution. |
| AGENT-MAP-03 | AGENT-03 / AGENT-04 / TOOL-05 | TH-07 / TH-12 | agent_tool_mcp_map.md; backend_architecture.md; rag_pipeline_map.md | backend/onyx/hooks/registry.py; backend/onyx/hooks/executor.py; backend/onyx/server/features/build/sandbox/util/agent_instructions.py; backend/onyx/server/features/build/sandbox/tasks/tasks.py | UNVERIFIED | The files suggest agent instructions, hook execution, and sandbox-related behavior, but they do not prove human approval or sandbox isolation. | No runtime approval or sandbox-isolation validation was collected. | Approval-flow and sandbox-isolation review. | Unverified because the control may exist but is not evidenced. |
