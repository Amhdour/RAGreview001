> This is the client-facing mirror of the PHASE 7 evidence file. The canonical evidence copy remains under rag-security-readiness-review/02_evidence/phase_7/.

# Agent Risks

## Category purpose

Capture risks introduced when LLM-driven or background agent behavior can act on retrieved context or invoke tools.

## Scope

Agent state, tool-use policy, retrieved-context use, and action authorization.

## Related PHASE 5 architecture evidence

- rag-security-readiness-review/02_evidence/phase_5/agent_tool_mcp_map.md
- rag-security-readiness-review/02_evidence/phase_5/backend_architecture.md
- rag-security-readiness-review/02_evidence/phase_5/rag_pipeline_map.md

## Related PHASE 6 threats

- TH-01
- TH-07
- TH-11
- TH-12

## Protected assets affected

Agent prompts/state; tool definitions; tool outputs; retrieved chunks; execution context

## Actors involved

Agent/tool executor; Tool/MCP caller; authenticated user; malicious insider

## Trust boundaries involved

Prompt/LLM; tool execution; ingestion; retrieval/search

## Data flows involved

Retrieval into agent context; agent to tool execution; tool output back into model or user response

## Risk list

| Risk ID | Risk | Evidence label | Related PHASE 6 threat ID | Related PHASE 5 evidence | Affected assets | Actors | Trust boundaries | Potential impact | Missing evidence | Later validation method | Priority |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| AGENT-01 | Agent action without clear authorization may trigger unintended side effects. | EVIDENCE-LINKED | TH-11 | agent_tool_mcp_map.md; backend_architecture.md; rag_pipeline_map.md | Agent prompts/state; tool definitions; tool outputs; retrieved chunks; execution context | Agent/tool executor; Tool/MCP caller; authenticated user; malicious insider | Prompt/LLM; tool execution; ingestion; retrieval/search | Unintended actions, data access, or downstream leakage. | No live tool-policy test. | Later tool/MCP policy review. | High candidate |
| AGENT-02 | Agent/tool output injection can alter later model or tool behavior. | EVIDENCE-LINKED | TH-07, TH-11 | agent_tool_mcp_map.md; backend_architecture.md; rag_pipeline_map.md | Agent prompts/state; tool definitions; tool outputs; retrieved chunks; execution context | Agent/tool executor; Tool/MCP caller; authenticated user; malicious insider | Prompt/LLM; tool execution; ingestion; retrieval/search | Unsafe output, disclosure, or tool misuse can cascade through the agent loop. | No runtime injection test. | Later prompt-injection review. | Critical candidate |
| AGENT-03 | Agent state confusion can mix instructions, context, or conversation boundaries. | INFERRED | TH-07, TH-12 | agent_tool_mcp_map.md; backend_architecture.md; rag_pipeline_map.md | Agent prompts/state; tool definitions; tool outputs; retrieved chunks; execution context | Agent/tool executor; Tool/MCP caller; authenticated user; malicious insider | Prompt/LLM; tool execution; ingestion; retrieval/search | State corruption may cause wrong tool selection or incorrect responses. | No direct agent state-invariant test. | Later agent state and context-handling review. | Medium candidate |
| AGENT-04 | Agent misuse of retrieved context may amplify a retrieval issue into an action issue. | EVIDENCE-LINKED | TH-01, TH-07 | agent_tool_mcp_map.md; backend_architecture.md; rag_pipeline_map.md | Agent prompts/state; tool definitions; tool outputs; retrieved chunks; execution context | Agent/tool executor; Tool/MCP caller; authenticated user; malicious insider | Prompt/LLM; tool execution; ingestion; retrieval/search | A prompt may reuse sensitive context in a way that widens exposure. | No live end-to-end agent execution evidence. | Later prompt-to-tool chain review. | High candidate |

## Missing evidence

No runtime agent policy validation; no live approval workflow validation for sensitive actions; no direct agent state-invariant testing.

## Later validation methods

Agent runtime-policy review; tool authorization and approval-flow validation; context-handling and state-confusion review.

## Non-claims

No claim that agent controls are verified; no claim of exploitability; no claim that tool scope is safe.

## Client-ready summary

The category shows how injected content, tool execution, and ambiguous agent state can widen the impact of retrieval or tool misuse.
