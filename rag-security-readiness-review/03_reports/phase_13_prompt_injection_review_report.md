# PHASE 13 — Prompt-Injection Exposure Review Report

## Executive summary
PHASE 13 reviewed the source-level flow of user prompts, system prompts, retrieved document content, citation/source metadata, tool instructions, and agent instructions. The review found multiple prompt-adjacent construction paths, but no runtime validation evidence showing a dedicated prompt-injection defense layer.

## Evidence basis
- Prior phase evidence from PHASE 12, PHASE 11, PHASE 10, PHASE 9, PHASE 8, PHASE 7, PHASE 6, PHASE 5, and PHASE 3.
- Local source inspection of chat, search, prompt, citation, tool, agent, sanitization, and test files.
- No application tests, CI, or exploit tests were run.

## Retrieved context construction summary
Retrieved context is built through the search pipeline, section ranking/expansion, context-file serialization, and LLM-facing search output. See `backend/onyx/tools/tool_implementations/search/search_tool.py:539-1002`, `backend/onyx/tools/tool_implementations/search/search_utils.py:28-470`, and `backend/onyx/chat/llm_loop.py:570-602`.

## System prompt construction summary
System prompts combine default chat prompts, persona prompts, citation reminders, tool guidance, and search templates. See `backend/onyx/chat/prompt_utils.py:47-280`, `backend/onyx/prompts/chat_prompts.py:13-125`, `backend/onyx/prompts/tool_prompts.py:3-78`, and `backend/onyx/prompts/search_prompts.py:15-196`.

## User prompt handling summary
User input is routed through chat request handling, history conversion, and search query construction. See `backend/onyx/chat/process_message.py:660-823`, `backend/onyx/chat/chat_utils.py:163-260,536-598`, and `backend/onyx/chat/llm_step.py:844-1002`.

## Retrieved document insertion summary
Retrieved chunks and context files are inserted into LLM-facing structures with titles, metadata, and content. See `backend/onyx/tools/tool_implementations/utils.py:21-119`, `backend/onyx/chat/llm_loop.py:570-602`, and `backend/onyx/tools/tool_implementations/search/search_tool.py:847-1002`.

## Citation/source insertion summary
Citation mapping and source display are preserved across tool output, chat output, and the frontend citation component. See `backend/onyx/chat/citation_processor.py:69-119,371+`, `backend/onyx/chat/citation_utils.py:10-221`, `backend/onyx/tools/tool_runner.py:228-447`, and `web/src/components/search/results/Citation.tsx:37-123`.

## Tool/agent instruction insertion summary
Tool guidance, MCP descriptions, and coding-agent prompts are all prompt material. See `backend/onyx/prompts/tool_prompts.py:3-78`, `backend/onyx/tools/tool_implementations/coding_agent/coding_agent_tool.py:84-193`, `backend/onyx/server/features/mcp/api.py:177-183,1764-1794`, and `backend/onyx/server/features/build/sandbox/util/agent_instructions.py:37-145`.

## Prompt template summary
Prompt templates are generic and reusable across chat, search, tool, and agent flows. See `backend/onyx/prompts/prompt_template.py:6-54`, `backend/onyx/prompts/chat_prompts.py:13-125`, `backend/onyx/prompts/chat_tools.py:9-97`, `backend/onyx/prompts/search_prompts.py:15-196`, and `backend/onyx/prompts/coding_agent/coding_agent.py:8-25`.

## Document text sanitization summary
Sanitization is visible in ingestion and storage paths, including unicode cleanup, HTML cleanup, and string sanitization. See `backend/onyx/utils/postgres_sanitization.py:15-49`, `backend/onyx/utils/text_processing.py:275-288`, `backend/onyx/file_processing/html_utils.py:27-223`, `backend/onyx/document_index/vespa/indexing_utils.py:167-205`, and `backend/onyx/document_index/opensearch/opensearch_document_index.py:196-214`.

## Prompt-injection controls summary
The reviewed sources show token budgets, ACL/doc-set filtering, result limits, and section selection. These are useful controls, but they are not proof of prompt-injection defense. See `backend/onyx/chat/prompt_utils.py:57-121`, `backend/onyx/chat/llm_loop.py:303-540`, `backend/onyx/context/search/preprocessing/access_filters.py:8-21`, `backend/onyx/context/search/pipeline.py:41-117`, `backend/onyx/tools/tool_implementations/search/search_tool.py:558-1002`, and `backend/onyx/secondary_llm_flows/document_filter.py:22-203`.

## Indirect prompt-injection controls summary
Uploaded files, connector content, and retrieved content can all reach the prompt-adjacent path. No dedicated scanner or quarantine path was identified. See `backend/onyx/chat/llm_loop.py:570-602`, `backend/onyx/file_processing/html_utils.py:27-223`, and `backend/onyx/tools/tool_implementations/search/search_utils.py:28-470`.

## Malicious retrieved-content controls summary
The reviewed sources show retrieval shaping but not malicious-instruction detection or quarantine. See `backend/onyx/secondary_llm_flows/document_filter.py:22-203` and `backend/onyx/tools/tool_implementations/search/search_utils.py:351-470`.

## Instruction hierarchy protections summary
System, user, retrieved, and tool content are represented separately in code, but no explicit anti-override policy was identified. See `backend/onyx/chat/prompt_utils.py:194-280`, `backend/onyx/chat/llm_loop.py:303-602`, and `backend/onyx/prompts/tool_prompts.py:3-78`.

## Context stuffing controls summary
Token budgeting, history truncation, reranking, and section limits exist. See `backend/onyx/chat/prompt_utils.py:57-121`, `backend/onyx/chat/chat_utils.py:536-598`, `backend/onyx/chat/llm_loop.py:303-540`, and `backend/onyx/tools/tool_implementations/search/search_tool.py:558-1002`.

## Source confusion controls summary
Source metadata and citation mappings are preserved, but no explicit source-integrity validation was identified. See `backend/onyx/chat/citation_utils.py:10-221`, `backend/onyx/tools/tool_implementations/utils.py:21-119`, and `web/src/components/search/results/Citation.tsx:37-123`.

## Citation spoofing controls summary
Citations are rendered and renumbered, but no dedicated anti-spoofing control was identified. See `backend/onyx/chat/citation_processor.py:69-119,371+` and `backend/onyx/chat/citation_utils.py:100-221`.

## Prompt-injection test summary
Several unit-test files cover prompt utilities, chat history, citations, search formatting, tool files, and MCP template behavior. They were discovered but not executed. See `backend/tests/unit/onyx/prompts/test_prompt_utils.py`, `backend/tests/unit/onyx/chat/test_chat_utils.py`, `backend/tests/unit/onyx/chat/test_citation_processor.py`, `backend/tests/unit/onyx/chat/test_citation_utils.py`, `backend/tests/unit/onyx/chat/test_llm_loop.py`, `backend/tests/unit/onyx/chat/test_context_files.py`, `backend/tests/unit/onyx/tools/test_search_llm_json.py`, `backend/tests/unit/onyx/tools/test_tool_runner_chat_files.py`, `backend/tests/unit/onyx/tools/test_search_utils.py`, and `backend/tests/unit/onyx/server/features/mcp/test_template_header_substitution.py`.

## Confirmed findings
- None confirmed from source-only evidence.

## Observations
- Prompt surfaces are explicitly assembled from system, user, retrieved, citation, tool, and agent content.
- Capacity and access controls exist throughout chat/search flows.
- Sanitization exists in ingestion/storage paths.
- Citation and source data are preserved through structured output.
- Prompt templates are reusable and broad.
- No dedicated prompt-injection scanner or policy engine was identified.
- No runtime validation evidence was collected.

## Unverified risks
- Retrieved text may carry malicious instructions into prompt context.
- Tool and agent instruction space may be vulnerable to instruction confusion.
- Citation/source spoofing remains plausible.
- Context stuffing could amplify malicious content exposure.
- Cross-document contamination remains plausible.
- No dedicated prompt-injection defense layer was identified in the reviewed sources.

## Missing evidence
- Runtime RAG, LLM, and tool behavior.
- Prompt-injection-specific tests.
- CI results.
- Production/live validation.

## Limitations
- Source-only review.
- Current checkout only.
- No tests or CI were run.
- No live environment evidence was collected.

## Non-claims
- No claim of exploitability.
- No claim of production readiness.
- No claim that prompt-injection controls are effective.
- No claim that any test passed.

## PHASE 13 status
- COMPLETE WITH LIMITATIONS

## Exact next phase
- PHASE 14 — Review citation and source integrity
