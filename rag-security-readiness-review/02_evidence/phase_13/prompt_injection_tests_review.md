# Prompt-Injection Tests Review

| Area | Test/evidence file | Test type | What it appears to cover | Was it executed? | Result evidence | Missing assertion | Limitation |
| ---- | ------------------ | --------- | ------------------------ | ---------------- | --------------- | ----------------- | ---------- |
| Prompt utilities | backend/tests/unit/onyx/prompts/test_prompt_utils.py | Unit | Reminder-tag and prompt utility behavior | NO | File exists only | No prompt-injection assertion | Not executed in this review |
| Chat history and prompt flow | backend/tests/unit/onyx/chat/test_chat_utils.py | Unit | History conversion and prompt helpers | NO | File exists only | No injection-specific assertion | Not executed in this review |
| Citation processor | backend/tests/unit/onyx/chat/test_citation_processor.py | Unit | Citation formatting/removal/linking | NO | File exists only | No spoofing adversary case | Not executed in this review |
| Citation utilities | backend/tests/unit/onyx/chat/test_citation_utils.py | Unit | Citation renumbering and extraction | NO | File exists only | No injection-specific assertion | Not executed in this review |
| LLM loop | backend/tests/unit/onyx/chat/test_llm_loop.py | Unit | Message-history construction and context handling | NO | File exists only | No malicious-context assertion | Not executed in this review |
| Context-file handling | backend/tests/unit/onyx/chat/test_context_files.py | Unit | Context file precedence / extraction | NO | File exists only | No malicious-file assertion | Not executed in this review |
| Search/tool JSON output | backend/tests/unit/onyx/tools/test_search_llm_json.py | Unit | Search LLM output formatting | NO | File exists only | No prompt-injection assertion | Not executed in this review |
| Tool runner chat files | backend/tests/unit/onyx/tools/test_tool_runner_chat_files.py | Unit | File handling in tool runner | NO | File exists only | No injection assertion | Not executed in this review |
| Search utilities | backend/tests/unit/onyx/tools/test_search_utils.py | Unit | RRF / section helpers | NO | File exists only | No injection assertion | Not executed in this review |
| MCP template handling | backend/tests/unit/onyx/server/features/mcp/test_template_header_substitution.py | Unit | Template substitution | NO | File exists only | No prompt-injection assertion | Not executed in this review |

## Notes
- The tests discovered here are relevant evidence files, not executed results.
- No dedicated prompt-injection exploit test or runtime validation evidence was found.
