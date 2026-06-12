# Prompt-Injection Risks

## Category purpose

Describe how malicious content can influence prompts, retrieval, or tool use.

## Scope

Prompt construction, retrieved-context assembly, instruction hierarchy, and injected tool directives.

## Related PHASE 5 architecture evidence

- rag-security-readiness-review/02_evidence/phase_5/backend_architecture.md
- rag-security-readiness-review/02_evidence/phase_5/rag_pipeline_map.md
- rag-security-readiness-review/02_evidence/phase_5/agent_tool_mcp_map.md

## Related PHASE 6 threats

- TH-01
- TH-07
- TH-10
- TH-11

## Protected assets affected

Prompts; retrieved chunks; tool instructions; chat outputs; tokens or sensitive prompt data

## Actors involved

External attacker; malicious insider; agent/tool executor; authenticated user

## Trust boundaries involved

Ingestion; retrieval/search; prompt/LLM; tool execution

## Data flows involved

Malicious content into retrieval context; prompt construction to model call; model output to tool execution

## Risk list

| Risk ID | Risk | Evidence label | Related PHASE 6 threat ID | Related PHASE 5 evidence | Affected assets | Actors | Trust boundaries | Potential impact | Missing evidence | Later validation method | Priority |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| PI-01 | Malicious document injection can place hostile instructions into the retrieval corpus. | EVIDENCE-LINKED | TH-07 | backend_architecture.md; rag_pipeline_map.md; agent_tool_mcp_map.md | Prompts; retrieved chunks; tool instructions; chat outputs; tokens or sensitive prompt data | External attacker; malicious insider; agent/tool executor; authenticated user | Ingestion; retrieval/search; prompt/LLM; tool execution | Downstream answers or tool behavior may become unsafe or misleading. | No runtime injection test. | Later prompt-injection review. | Critical candidate |
| PI-02 | Indirect prompt injection through retrieval can carry hostile instructions into model context. | EVIDENCE-LINKED | TH-07, TH-01 | backend_architecture.md; rag_pipeline_map.md; agent_tool_mcp_map.md | Prompts; retrieved chunks; tool instructions; chat outputs; tokens or sensitive prompt data | External attacker; malicious insider; agent/tool executor; authenticated user | Ingestion; retrieval/search; prompt/LLM; tool execution | An answer may reflect attacker-supplied instructions instead of user intent. | No retrieval-context red-team test. | Later retrieval-context injection review. | High candidate |
| PI-03 | Prompt/context construction abuse can reshape instructions or hide higher-priority guidance. | INFERRED | TH-07, TH-11 | backend_architecture.md; rag_pipeline_map.md; agent_tool_mcp_map.md | Prompts; retrieved chunks; tool instructions; chat outputs; tokens or sensitive prompt data | External attacker; malicious insider; agent/tool executor; authenticated user | Ingestion; retrieval/search; prompt/LLM; tool execution | The prompt assembly logic may be manipulated by crafted content. | No prompt-construction audit. | Later prompt-construction review. | High candidate |
| PI-04 | Tool-use escalation through injected content can turn a text issue into an action issue. | EVIDENCE-LINKED | TH-07, TH-11 | backend_architecture.md; rag_pipeline_map.md; agent_tool_mcp_map.md | Prompts; retrieved chunks; tool instructions; chat outputs; tokens or sensitive prompt data | External attacker; malicious insider; agent/tool executor; authenticated user | Ingestion; retrieval/search; prompt/LLM; tool execution | Injected text may trigger unintended tool calls or later-stage actions. | No runtime prompt-to-tool chain test. | Later prompt-escalation review. | Critical candidate |
| PI-05 | Sensitive prompt data can leak into logs or telemetry as part of prompt tracing. | EVIDENCE-LINKED | TH-10 | backend_architecture.md; rag_pipeline_map.md; agent_tool_mcp_map.md | Prompts; retrieved chunks; tool instructions; chat outputs; tokens or sensitive prompt data | External attacker; malicious insider; agent/tool executor; authenticated user | Ingestion; retrieval/search; prompt/LLM; tool execution | Private content may become visible outside the user-facing flow. | No live observability review. | Later redaction review. | High candidate |

## Missing evidence

No runtime prompt-injection test; no validation of instruction hierarchy handling; no live review of prompt redaction or leakage controls.

## Later validation methods

Prompt-injection red-team review; instruction hierarchy and context-building review; tool-escalation validation using safe test cases.

## Non-claims

No claim that injection resistance is proven; no claim that tool escalation was demonstrated; no claim that prompt secrecy is guaranteed.

## Client-ready summary

This category records how untrusted content can reshape model behavior even when the underlying source evidence is only static.
