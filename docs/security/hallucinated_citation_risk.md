> This is the client-facing mirror of the PHASE 14 citation/source integrity review file. The canonical evidence copy remains under rag-security-readiness-review/02_evidence/phase_14/.


# Hallucinated Citation Risk

| Risk path | File/path evidence | What is confirmed | What is unverified | Potential impact | Later validation method |
| --------- | ------------------ | ----------------- | ------------------ | ---------------- | ----------------------- |
| LLM-generated citations | `backend/onyx/chat/citation_processor.py`; `backend/onyx/chat/llm_loop.py` | Citation output is transformed from model text using a citation map | Whether the model invents unsupported citations at runtime | Users may see citations that are not grounded in retrieved sources | Execute chat streaming tests with controlled retrieved documents and invalid citation outputs |
| Citation target mismatch | `backend/onyx/chat/citation_processor.py`; `backend/onyx/chat/citation_utils.py` | Missing citation numbers are skipped; renumbering uses document IDs | Whether every displayed citation always points to the intended source | Wrong or confusing source association | Validate citation mapping against known document IDs in runtime tests |
| Missing source handling | `backend/onyx/chat/citation_processor.py` | Unknown citation numbers are logged and ignored | Whether the user-visible answer still implies a valid source | Answers may appear to cite a source that is absent from the final map | Add runtime assertions for missing citation targets |
| Citation marker mismatch | `backend/onyx/chat/citation_processor.py`; `backend/onyx/chat/citation_utils.py` | Regex-based marker parsing handles ASCII and Unicode bracket forms | Whether malformed markers can still confuse readers | Citation confusion or rendering inconsistency | Fuzz the processor with malformed and partial citation markers |
| Answer referencing nonexistent source | `backend/onyx/chat/citation_processor.py`; `backend/onyx/chat/llm_loop.py` | Backend can only emit citations it has mapped | Whether the final answer text can still imply nonexistent evidence | Misleading answer trust | Compare answer text, citation info, and source map in integration tests |
| Tests for hallucinated citations if present | `backend/tests/unit/onyx/chat/test_citation_processor.py`; `backend/tests/unit/onyx/chat/test_citation_utils.py` | Extensive unit tests exist for parsing and renumbering | Whether the tests were executed in this review | Test presence does not prove runtime defense | Run the discovered unit tests in a controlled environment |
