> This is the client-facing mirror of the PHASE 13 prompt-injection review file. The canonical evidence copy remains under rag-security-readiness-review/02_evidence/phase_13/.

# Instruction Hierarchy Protections

## System vs user vs retrieved content separation
- System prompts are built separately from user history and retrieved context. `backend/onyx/chat/prompt_utils.py:194-280`; `backend/onyx/chat/llm_loop.py:303-602`.
- Retrieved content is serialized as context documents or search-doc output rather than merged into the base system prompt body alone. `backend/onyx/chat/llm_loop.py:570-602`; `backend/onyx/tools/tool_implementations/utils.py:21-119`.

## Tool/agent instruction separation
- Tool guidance, agent prompts, and MCP descriptions are source-controlled but can enter prompt-adjacent flows. `backend/onyx/prompts/tool_prompts.py:3-78`; `backend/onyx/prompts/coding_agent/coding_agent.py:8-25`; `backend/onyx/server/features/mcp/api.py:177-183,1764-1794`.
- No explicit hierarchy policy or anti-override gate was identified.

## Explicit untrusted-content warnings
- The reviewed sources include contextual framing such as “provided for context,” but no explicit untrusted-content warning was identified as a general anti-injection control. `backend/onyx/chat/llm_loop.py:570-602`.

## Anti-override instructions
- The base prompts include strong assistant guidance and citation/tool reminders. `backend/onyx/prompts/chat_prompts.py:13-125`; `backend/onyx/chat/prompt_utils.py:194-280`.
- No source-only evidence showed a special anti-override instruction protecting against prompt injection.

## Missing evidence
- No dedicated instruction-hierarchy test was identified.

## Unverified risks
- Retrieved text, tool instructions, and user text may still compete in the same model context.
- A document or tool output containing instructions could be interpreted as higher-priority content by the model.
