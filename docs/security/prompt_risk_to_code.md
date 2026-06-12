> This is the client-facing mirror of the PHASE 8 evidence file. The canonical evidence copy remains under rag-security-readiness-review/02_evidence/phase_8/.

# Prompt/Context Risk to Code

## Category purpose
Map prompt assembly, context construction, citation formatting, and LLM orchestration code that can influence instruction hierarchy and model inputs.

## Related PHASE 7 risks
- PI-01
- PI-02
- PI-03
- PI-04
- PI-05
- AGENT-02
- RAG-03

## Related PHASE 6 threats
- TH-01
- TH-07
- TH-10
- TH-11

## Related PHASE 5 architecture evidence
- rag-security-readiness-review/02_evidence/phase_5/backend_architecture.md
- rag-security-readiness-review/02_evidence/phase_5/rag_pipeline_map.md
- rag-security-readiness-review/02_evidence/phase_5/agent_tool_mcp_map.md

## Related PHASE 3 inventory evidence
- rag-security-readiness-review/02_evidence/phase_3/baseline_inventory.md
- rag-security-readiness-review/02_evidence/phase_3/important_files_index.md
- rag-security-readiness-review/02_evidence/phase_3/security_relevant_files.md

## Candidate Onyx file paths
- backend/onyx/chat/process_message.py
- backend/onyx/chat/prompt_utils.py
- backend/onyx/chat/llm_step.py
- backend/onyx/chat/llm_loop.py
- backend/onyx/chat/citation_processor.py
- backend/onyx/chat/citation_utils.py
- backend/onyx/chat/chat_utils.py
- backend/onyx/chat/compression.py
- backend/onyx/tracing/flows.py
- backend/onyx/tracing/masking.py
- backend/onyx/tracing/llm_utils.py

## Existing control candidates
- PROMPT-MAP-01: prompt construction and message orchestration paths appear present.
- PROMPT-MAP-02: citation and tracing/masking paths appear present.

## Missing control candidates
- No dedicated runtime proof of prompt hierarchy or masking effectiveness was collected.

## Unverified mappings
- PROMPT-MAP-03: context assembly and masking remain unverified.

## Later validation methods
- Prompt hierarchy and context assembly review.
- Tracing and masking validation.
- Citation formatting review.

## Non-claims
- No claim that prompt construction is secure.
- No claim that redaction is complete.

## Client-ready summary
Prompt and context handling appear to be implemented in several chat and tracing files, but their effectiveness is not validated here.

## Mapping table

| Mapping ID | Related risk ID/category | Related PHASE 6 threat ID | Related PHASE 5 architecture evidence | Candidate Onyx file/path | Mapping label | Why this file/path matters | Missing evidence | Later validation method | Notes |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| PROMPT-MAP-01 | PI-01 / PI-02 | TH-07 | backend_architecture.md; rag_pipeline_map.md; agent_tool_mcp_map.md | backend/onyx/chat/process_message.py; backend/onyx/chat/prompt_utils.py; backend/onyx/chat/llm_step.py; backend/onyx/chat/llm_loop.py | EXISTING-CANDIDATE | These files are the clearest prompt-construction and message-orchestration candidate paths in the current checkout. | No runtime prompt-injection or context-ordering test was performed. | Prompt-construction audit and retrieved-context formatting review. | Source-level prompt assembly candidate only. |
| PROMPT-MAP-02 | PI-04 / PI-05 | TH-10 | backend_architecture.md; rag_pipeline_map.md; agent_tool_mcp_map.md | backend/onyx/chat/citation_processor.py; backend/onyx/chat/citation_utils.py; backend/onyx/chat/chat_utils.py; backend/onyx/tracing/flows.py; backend/onyx/tracing/masking.py | EXISTING-CANDIDATE | These paths suggest the formatting and tracing steps where citations, prompts, and redaction can be assembled or masked. | No live tracing or masking proof was collected. | Prompt-to-telemetry redaction validation. | Relevant to prompt leakage and citation formatting. |
| PROMPT-MAP-03 | PI-03 | TH-10 / TH-11 | backend_architecture.md; rag_pipeline_map.md; agent_tool_mcp_map.md | backend/onyx/tracing/flows.py; backend/onyx/tracing/masking.py; backend/onyx/chat/llm_loop.py | UNVERIFIED | The files are consistent with prompt/context orchestration, but source-only evidence cannot confirm the instruction hierarchy or masking effectiveness. | No runtime prompt-construction or masking validation was collected. | Prompt hierarchy, context assembly, and redaction runtime review. | Unverified because later validation is still needed. |
