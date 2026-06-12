> This is the client-facing mirror of the PHASE 7 evidence file. The canonical evidence copy remains under rag-security-readiness-review/02_evidence/phase_7/.

# Tool/MCP Risks

## Category purpose

Describe risks around tool registration, MCP exposure, and tool execution control.

## Scope

Tool APIs, MCP routes, tool registries, and execution policy enforcement.

## Related PHASE 5 architecture evidence

- rag-security-readiness-review/02_evidence/phase_5/agent_tool_mcp_map.md
- rag-security-readiness-review/02_evidence/phase_5/api_routes_map.md
- rag-security-readiness-review/02_evidence/phase_5/backend_architecture.md

## Related PHASE 6 threats

- TH-07
- TH-11

## Protected assets affected

Tool definitions; MCP routes; tool outputs; execution policy; downstream actions

## Actors involved

Tool/MCP caller; agent/tool executor; authenticated user; malicious insider

## Trust boundaries involved

Tool execution; MCP; prompt/LLM

## Data flows involved

Caller request into tool API; tool output into agent or user response; MCP route to backend execution

## Risk list

| Risk ID | Risk | Evidence label | Related PHASE 6 threat ID | Related PHASE 5 evidence | Affected assets | Actors | Trust boundaries | Potential impact | Missing evidence | Later validation method | Priority |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| TOOL-01 | Unauthorized tool execution can run actions outside the expected chat flow. | EVIDENCE-LINKED | TH-11 | agent_tool_mcp_map.md; api_routes_map.md | Tool definitions; MCP routes; tool outputs; execution policy; downstream actions | Tool/MCP caller; agent/tool executor; authenticated user; malicious insider | Tool execution; MCP; prompt/LLM | Data access or actions may execute without the intended gate. | No live tool/MCP authorization validation. | Later tool-authorization review. | Critical candidate |
| TOOL-02 | MCP endpoint or tool exposure can broaden the reachable backend attack surface. | EVIDENCE-LINKED | TH-11 | agent_tool_mcp_map.md; api_routes_map.md | Tool definitions; MCP routes; tool outputs; execution policy; downstream actions | Tool/MCP caller; agent/tool executor; authenticated user; malicious insider | Tool execution; MCP; prompt/LLM | More requests or data paths may be reachable than intended. | No live endpoint exposure review. | Later MCP endpoint review. | High candidate |
| TOOL-03 | Tool output injection can contaminate later prompts, chats, or actions. | EVIDENCE-LINKED | TH-11, TH-07 | agent_tool_mcp_map.md; api_routes_map.md | Tool definitions; MCP routes; tool outputs; execution policy; downstream actions | Tool/MCP caller; agent/tool executor; authenticated user; malicious insider | Tool execution; MCP; prompt/LLM | Injected tool results may change later behavior or disclosures. | No runtime injection test. | Later tool-output review. | High candidate |
| TOOL-04 | Tool registry confusion can blur which operations are allowed or trusted. | INFERRED | TH-11 | agent_tool_mcp_map.md; api_routes_map.md | Tool definitions; MCP routes; tool outputs; execution policy; downstream actions | Tool/MCP caller; agent/tool executor; authenticated user; malicious insider | Tool execution; MCP; prompt/LLM | The wrong tool may be selected or treated as trusted by mistake. | No registry audit. | Later tool-registry review. | Medium candidate |
| TOOL-05 | Missing approval workflow for sensitive tool actions remains unverified. | UNVERIFIED | TH-11 | agent_tool_mcp_map.md; api_routes_map.md | Tool definitions; MCP routes; tool outputs; execution policy; downstream actions | Tool/MCP caller; agent/tool executor; authenticated user; malicious insider | Tool execution; MCP; prompt/LLM | Sensitive actions may proceed without an extra human gate. | No approval-workflow validation. | Later approval-workflow review. | Informational |

## Missing evidence

No live tool/MCP authorization validation; no approval-workflow validation; no runtime tool-policy enforcement review.

## Later validation methods

Tool authorization review; MCP endpoint validation; runtime tool-policy inspection and safe execution tests.

## Non-claims

No claim that tool execution is safe; no claim that MCP exposure is acceptable; no claim that runtime policy is verified.

## Client-ready summary

The category isolates direct tool execution and MCP exposure from broader agent or prompt concerns.
