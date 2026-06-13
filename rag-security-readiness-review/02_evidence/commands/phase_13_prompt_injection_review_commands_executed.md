# PHASE 13 Prompt-Injection Review Commands Executed

This log records the source-only inspection commands used for PHASE 13. No application tests, CI, or exploit tests were run.

## Repository / environment checks
- `pwd`
- `git rev-parse --show-toplevel`
- `git branch --show-current`
- `git rev-parse HEAD`
- `git status --short`
- `find .. -name AGENTS.md -print`

## Prior-phase evidence inventory
- `find rag-security-readiness-review/02_evidence/phase_12 -maxdepth 3 -type f | sort`
- `find rag-security-readiness-review/02_evidence/phase_11 -maxdepth 3 -type f | sort`
- `find rag-security-readiness-review/02_evidence/phase_10 -maxdepth 3 -type f | sort`
- `find rag-security-readiness-review/02_evidence/phase_9 -maxdepth 3 -type f | sort`
- `find rag-security-readiness-review/02_evidence/phase_8 -maxdepth 3 -type f | sort`
- `find rag-security-readiness-review/02_evidence/phase_5 -maxdepth 2 -type f | sort`

## Source search / inspection commands
- `rg --files backend web docs rag-security-readiness-review/02_evidence | rg -i "prompt|context|retrieved|chunk|section|document|source|citation|answer|llm|model|message|chat|persona|project|doc_set|document_set|attached|tool|agent|mcp|function_call|action|instruction|hierarchy|injection|malicious|sanitize|strip|markdown|html|script|redact|filter|scanner|guardrail|firewall|policy|block|monitor|spoof|delimiter|untrusted|trusted" | sort`
- `rg -n -i "prompt|prompts|system_prompt|system prompt|user prompt|user_prompt|context|retrieved|retrieved_context|chunk|section|document|source|citation|citations|answer|llm|model|message|chat|persona|project|doc_set|document_set|attached_document|tool|tools|agent|agents|mcp|function_call|action|instruction|instructions|hierarchy|injection|prompt injection|indirect|malicious|sanitize|sanitization|strip|markdown|html|script|redact|redaction|filter|scanner|guardrail|llama|firewall|policy|block|monitor|context stuffing|source confusion|citation spoofing|spoof|delimiter|quote|untrusted|trusted" backend web docs rag-security-readiness-review/02_evidence 2>/dev/null || true`
- `find backend/tests web/tests tests -type f 2>/dev/null | sort`
- `rg -n -i "prompt|injection|rag|context|citation|source|tool|agent|mcp|malicious|sanitize|guardrail|scanner|spoof|stuffing|untrusted" backend/tests web/tests tests 2>/dev/null || true`

## Direct file inspection used for evidence notes
- `nl -ba backend/onyx/chat/prompt_utils.py | sed -n '1,320p'`
- `nl -ba backend/onyx/prompts/chat_prompts.py | sed -n '1,220p'`
- `nl -ba backend/onyx/prompts/tool_prompts.py | sed -n '1,220p'`
- `nl -ba backend/onyx/prompts/search_prompts.py | sed -n '1,260p'`
- `nl -ba backend/onyx/prompts/prompt_template.py | sed -n '1,220p'`
- `nl -ba backend/onyx/prompts/chat_tools.py | sed -n '1,220p'`
- `nl -ba backend/onyx/prompts/coding_agent/coding_agent.py | sed -n '1,120p'`
- `nl -ba backend/onyx/server/features/build/sandbox/util/agent_instructions.py | sed -n '1,240p'`
- `nl -ba backend/onyx/tools/tool_implementations/coding_agent/coding_agent_tool.py | sed -n '1,240p'`
- `nl -ba backend/onyx/server/features/mcp/api.py | sed -n '160,260p;1750,1810p'`
- `nl -ba backend/onyx/tools/tool_runner.py | sed -n '220,470p'`
- `nl -ba backend/onyx/tools/tool_implementations/search/search_tool.py | sed -n '400,1020p'`
- `nl -ba backend/onyx/tools/tool_implementations/search/search_utils.py | sed -n '1,520p'`
- `nl -ba backend/onyx/secondary_llm_flows/document_filter.py | sed -n '1,260p'`
- `nl -ba backend/onyx/context/search/models.py | sed -n '1,320p'`
- `nl -ba backend/onyx/context/search/utils.py | sed -n '1,260p'`
- `nl -ba backend/onyx/context/search/preprocessing/access_filters.py | sed -n '1,120p'`
- `nl -ba backend/onyx/context/search/pipeline.py | sed -n '1,220p'`
- `nl -ba backend/onyx/server/query_and_chat/chat_backend.py | sed -n '100,860p'`
- `nl -ba backend/onyx/chat/chat_utils.py | sed -n '150,620p;880,1010p'`
- `nl -ba backend/onyx/chat/llm_step.py | sed -n '840,1010p'`
- `nl -ba backend/onyx/chat/llm_loop.py | sed -n '300,860p'`
- `nl -ba backend/onyx/chat/process_message.py | sed -n '280,840p;1000,1920p'`
- `nl -ba backend/onyx/chat/citation_processor.py | sed -n '1,460p'`
- `nl -ba backend/onyx/chat/citation_utils.py | sed -n '1,260p'`
- `nl -ba backend/onyx/tools/tool_implementations/utils.py | sed -n '1,220p'`
- `nl -ba backend/onyx/utils/postgres_sanitization.py | sed -n '1,120p'`
- `nl -ba backend/onyx/utils/text_processing.py | sed -n '260,320p'`
- `nl -ba backend/onyx/document_index/vespa/indexing_utils.py | sed -n '150,230p'`
- `nl -ba backend/onyx/document_index/opensearch/opensearch_document_index.py | sed -n '180,240p'`
- `nl -ba backend/onyx/file_processing/html_utils.py | sed -n '1,260p'`
- `nl -ba backend/tests/unit/onyx/prompts/test_prompt_utils.py | sed -n '1,220p'`
- `nl -ba backend/tests/unit/onyx/chat/test_chat_utils.py | sed -n '1,260p'`
- `nl -ba backend/tests/unit/onyx/chat/test_citation_processor.py | sed -n '1,260p'`
- `nl -ba backend/tests/unit/onyx/chat/test_citation_utils.py | sed -n '1,220p'`
- `nl -ba backend/tests/unit/onyx/chat/test_llm_loop.py | sed -n '1,260p;720,980p'`
- `nl -ba backend/tests/unit/onyx/chat/test_context_files.py | sed -n '1,260p'`
- `nl -ba backend/tests/unit/onyx/server/query_and_chat/test_query_and_chat_chat_utils.py | sed -n '1,220p'`
- `nl -ba backend/tests/unit/onyx/tools/test_tool_runner_chat_files.py | sed -n '1,260p'`
- `nl -ba backend/tests/unit/onyx/tools/test_search_llm_json.py | sed -n '1,360p'`
- `nl -ba backend/tests/unit/onyx/tools/test_search_utils.py | sed -n '1,260p'`
- `nl -ba backend/tests/unit/onyx/server/features/mcp/test_template_header_substitution.py | sed -n '1,220p'`

## No tests run
- No application tests were executed.
- No CI was executed.
- No exploit tests were executed.
