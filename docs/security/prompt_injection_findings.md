> This is the client-facing mirror of the PHASE 13 prompt-injection review file. The canonical evidence copy remains under rag-security-readiness-review/02_evidence/phase_13/.

# Prompt-Injection Findings

## Confirmed findings
- None confirmed from source-only evidence.

## Observations

### O-1 System prompts are composed from several source-controlled fragments
- Status: OBSERVATION
- Evidence: backend/onyx/chat/prompt_utils.py:47-280; backend/onyx/prompts/chat_prompts.py:13-125; backend/onyx/prompts/tool_prompts.py:3-78; backend/onyx/chat/llm_loop.py:613-845
- Meaning: Base prompt, persona prompt, citation guidance, tool guidance, and reminders are combined before model calls.
- Limitation: Composition exists, but runtime injection resistance is not proven.

### O-2 Retrieved content is explicitly inserted into LLM-facing context
- Status: OBSERVATION
- Evidence: backend/onyx/tools/tool_implementations/search/search_tool.py:539-1002; backend/onyx/tools/tool_implementations/search/search_utils.py:28-470; backend/onyx/context/search/models.py:64-241; backend/onyx/context/search/utils.py:56-211; backend/onyx/context/search/pipeline.py:41-117; backend/onyx/context/search/preprocessing/access_filters.py:8-21; backend/onyx/tools/tool_implementations/utils.py:21-119; backend/onyx/chat/llm_loop.py:570-602; backend/onyx/tools/tool_implementations/search/search_tool.py:847-1002
- Meaning: Search results, context files, and expanded sections become prompt-adjacent content.
- Limitation: No dedicated malicious-content filter was identified.

### O-3 User prompt/history flows directly into the model input path
- Status: OBSERVATION
- Evidence: backend/onyx/chat/process_message.py:660-823; backend/onyx/chat/llm_step.py:844-1002; backend/onyx/chat/chat_utils.py:163-260,536-598
- Meaning: User text is converted into model messages and can influence retrieval.
- Limitation: No prompt-injection validation evidence exists.

### O-4 Citation/source metadata is preserved and rendered
- Status: OBSERVATION
- Evidence: backend/onyx/chat/citation_processor.py:69-119,371+; backend/onyx/chat/citation_utils.py:10-221; backend/onyx/tools/tool_runner.py:228-447; backend/onyx/tools/tool_implementations/utils.py:21-119
- Meaning: Tool output, citation processors, and UI components all carry source metadata forward.
- Limitation: Integrity of the metadata is not runtime-validated here.

### O-5 Tool and agent instructions are prompt material
- Status: OBSERVATION
- Evidence: backend/onyx/prompts/tool_prompts.py:3-78; backend/onyx/tools/tool_runner.py:228-447; backend/onyx/tools/tool_implementations/coding_agent/coding_agent_tool.py:84-193; backend/onyx/server/features/mcp/api.py:177-183,1764-1794; backend/onyx/server/features/build/sandbox/util/agent_instructions.py:37-145
- Meaning: Tool guidance, agent prompts, and MCP descriptions are injected into instruction space.
- Limitation: No runtime prompt-injection boundary was identified.

### O-6 Sanitization exists for ingestion/storage, not as a proven prompt defense
- Status: OBSERVATION
- Evidence: backend/onyx/utils/postgres_sanitization.py:15-49; backend/onyx/utils/text_processing.py:275-288; backend/onyx/document_index/vespa/indexing_utils.py:167-205; backend/onyx/document_index/opensearch/opensearch_document_index.py:196-214; backend/onyx/file_processing/html_utils.py:27-223
- Meaning: Some text normalization occurs before storage/indexing.
- Limitation: This does not prove prompt-injection protection before model invocation.

### O-7 Context and token budgets are enforced
- Status: OBSERVATION
- Evidence: backend/onyx/chat/llm_loop.py:303-602; backend/onyx/chat/chat_utils.py:536-598; backend/onyx/chat/prompt_utils.py:57-280; backend/onyx/tools/tool_implementations/search/search_tool.py:558-1002; backend/onyx/tools/tool_implementations/search/search_utils.py:28-470; backend/onyx/secondary_llm_flows/document_filter.py:22-203
- Meaning: History, retrieval, and document inclusion are bounded.
- Limitation: Capacity limits do not equal injection defense.

## Unverified risks

### R-1 Retrieved content may carry malicious instructions into prompt context
- Status: UNVERIFIED-RISK
- Why unverified: Source-only evidence shows insertion, not runtime malicious-instruction blocking.
- Missing evidence: Runtime RAG behavior, prompt-injection tests, or scanner output.
- Later validation method: Controlled runtime review of retrieved-content handling with non-destructive test documents.
- Client-ready wording: Retrieved document text is allowed into LLM-facing context, so malicious instructions remain a review item.

### R-2 Tool and agent outputs may introduce instruction confusion
- Status: UNVERIFIED-RISK
- Why unverified: Tool descriptions and outputs are inserted, but safety enforcement is not shown.
- Missing evidence: Tool/agent runtime validation and policy evidence.
- Later validation method: Runtime review of tool call boundaries and approvals.
- Client-ready wording: Tool and agent instructions are part of the prompt surface and need runtime validation.

### R-3 Citation/source spoofing remains plausible
- Status: UNVERIFIED-RISK
- Why unverified: Source metadata is preserved and rendered, but integrity checks were not identified.
- Missing evidence: Citation-spoofing tests and source-integrity checks.
- Later validation method: Review citation rendering and source validation paths.
- Client-ready wording: Source labels and citations appear to be presentation data, not proven trust anchors.

### R-4 Context stuffing could amplify malicious content exposure
- Status: UNVERIFIED-RISK
- Why unverified: Token and section limits exist, but adversarial behavior was not tested.
- Missing evidence: Long-context adversarial tests.
- Later validation method: Non-destructive stress tests on prompt-size and section expansion.
- Client-ready wording: Large-context handling is bounded, but the safety effect is unproven.

### R-5 No dedicated prompt-injection scanner or policy engine was found
- Status: UNVERIFIED-RISK
- Why unverified: Absence of evidence is not proof of absence.
- Missing evidence: Explicit detector, scanner, or policy engine source.
- Later validation method: Broader codebase audit plus runtime review.
- Client-ready wording: The reviewed sources did not show a dedicated prompt-injection defense layer.

### R-6 Cross-document contamination remains plausible
- Status: UNVERIFIED-RISK
- Why unverified: Multiple chunks/documents can be merged and expanded.
- Missing evidence: Runtime controls preventing instruction bleed across documents.
- Later validation method: Review expanded retrieval behavior and context assembly with benign test content.
- Client-ready wording: Merged retrieved context may mix trusted and untrusted text.

## No-evidence-found areas
- Dedicated prompt-injection detector.
- Retrieved-context filter specifically for malicious instructions.
- Model-output scanner for prompt-injection content.
- Explicit instruction-hierarchy policy text.
- Citation-spoofing validation tests with execution evidence.
- Prompt-injection-specific runtime test execution evidence.
