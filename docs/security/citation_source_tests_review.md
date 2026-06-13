> This is the client-facing mirror of the PHASE 14 citation/source integrity review file. The canonical evidence copy remains under rag-security-readiness-review/02_evidence/phase_14/.


# Citation/Source Tests Review

| Area | Test/evidence file | Test type | What it appears to cover | Was it executed? | Result evidence | Missing assertion | Limitation |
| ---- | ------------------ | --------- | ------------------------ | ---------------- | --------------- | ----------------- | ---------- |
| Citation processor | `backend/tests/unit/onyx/chat/test_citation_processor.py` | Unit | Citation parsing, mode handling, deduplication, Unicode brackets, and code-block behavior | NO | None in this review | Runtime citation-output validation | Discovered only; not executed |
| Citation utilities | `backend/tests/unit/onyx/chat/test_citation_utils.py` | Unit | Citation renumbering and document ID reuse | NO | None in this review | End-to-end source attribution validation | Discovered only; not executed |
| Chat context files | `backend/tests/unit/onyx/chat/test_context_files.py` | Unit | Context-file extraction and metadata handling | NO | None in this review | Source-display or citation rendering assertions | Not a citation runtime test |
| Chat utils | `backend/tests/unit/onyx/chat/test_chat_utils.py` | Unit | Chat helper behavior with message composition and state | NO | None in this review | Citation/source integrity assertions | Discovered only; not executed |
| Search/tool runner | `backend/tests/unit/onyx/tools/test_tool_runner_chat_files.py`; `backend/tests/unit/onyx/tools/test_search_utils.py`; `backend/tests/unit/onyx/tools/test_search_llm_json.py` | Unit | Search-to-tool output and chat-file helpers | NO | None in this review | Source-to-display runtime checks | Discovered only; not executed |
| Frontend citation rendering | `web/tests/e2e/chat/chat_message_rendering.spec.ts` | E2E | Chat message rendering with cited web and internal documents | NO | None in this review | Live source authorization and stale-source handling | Discovered only; not executed |
| Existing evidence files | `rag-security-readiness-review/02_evidence/phase_13/*`; `rag-security-readiness-review/02_evidence/phase_12/*`; `rag-security-readiness-review/02_evidence/phase_11/*` | Source evidence | Prior phase architecture and risk mapping | YES, as source references only | Prior phase reports and evidence files exist | Runtime test execution | Source-only references are not execution proof |
