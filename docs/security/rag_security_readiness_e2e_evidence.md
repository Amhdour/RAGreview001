# RAG Security Readiness Review — Targeted + Controlled E2E Evidence

Date: 2026-06-13
Repository: `Amhdour/RAGreview001`
Branch: `main`

## Commit summary

| Commit | Change |
|---|---|
| `257855f0dc487aa68aa7aabb9f4187d82b45bfca` | Fixed prompt-context fence escape in `backend/onyx/prompts/prompt_utils.py`. |
| `78cb9cba295b016b0a8ac0af78f697ae8e39889d` | Added regression test for retrieved-document Markdown fence escape. |
| `55317d8f7c4a0f8102520453d41bf879e255c173` | Added controlled E2E RAG security test for ingestion, vector-style retrieval, ACL filtering, tenant filtering, deleted/private filtering, and prompt construction. |

## Control traceability matrix

| Control ID | Scenario | Evidence file | Status | Notes |
|---|---|---|---:|---|
| RAG-PI-001 | Retrieved document injection text cannot escape prompt context | `backend/onyx/prompts/prompt_utils.py`; `backend/tests/unit/onyx/prompts/test_prompt_context_fence_escape.py` | Implemented | Nested Markdown fence delimiters are neutralized before retrieved content is wrapped in the LLM context block. |
| RAG-E2E-001 | Ingestion -> retrieval -> ACL filtering -> prompt construction | `backend/tests/unit/onyx/security/test_rag_security_controlled_e2e.py` | Implemented | Controlled in-process E2E proof using deterministic vector-style retrieval and real ACL/prompt/ingestion helper functions. |
| RAG-ACL-001 | Cross-user private document retrieval is denied | `backend/tests/unit/onyx/security/test_rag_security_controlled_e2e.py` | Implemented | Alice's ACL cannot access Bob-only private document content. |
| RAG-TENANT-001 | Cross-tenant document retrieval is denied | `backend/tests/unit/onyx/security/test_rag_security_controlled_e2e.py` | Implemented | Tenant B document is retrieved as a candidate but filtered out for tenant A. |
| RAG-VDB-001 | Deleted/private vector candidate is filtered out | `backend/tests/unit/onyx/security/test_rag_security_controlled_e2e.py` | Implemented | Hidden/deleted candidate is excluded before prompt construction. |
| RAG-ING-001 | Malformed document ingestion is blocked or sanitized | `backend/tests/unit/onyx/security/test_rag_security_controlled_e2e.py` | Implemented | Malformed PDF extracts empty text/metadata/images; path-traversal filename is sanitized. |
| RAG-CITE-001 | Citation spoofing attempt is not accepted as a valid source | Existing citation tests: `backend/tests/unit/onyx/chat/test_citation_processor.py`, `backend/tests/unit/onyx/chat/test_citation_utils.py` | Existing evidence | Existing tests cover citation processor/source handling. |
| RAG-TOOL-001 | Tool network guard denies unsafe local/private targets | Existing tool-network test: `backend/tests/unit/onyx/tools/tool_implementations/mcp/test_mcp_ssrf.py` | Existing evidence | Existing repository test remains the evidence path for tool-network guard behavior. |

## Run commands

Run the new tests:

```bash
PYTHONPATH=backend pytest -q backend/tests/unit/onyx/prompts/test_prompt_context_fence_escape.py backend/tests/unit/onyx/security/test_rag_security_controlled_e2e.py
```

Recommended expanded security run:

```bash
PYTHONPATH=backend pytest -q backend/tests/unit/onyx/prompts/test_prompt_context_fence_escape.py backend/tests/unit/onyx/security/test_rag_security_controlled_e2e.py backend/tests/unit/onyx/chat/test_citation_processor.py backend/tests/unit/onyx/chat/test_citation_utils.py backend/tests/unit/onyx/tools/tool_implementations/mcp/test_mcp_ssrf.py
```

## Honest limitation

This is controlled unit/E2E evidence. It does not start OpenSearch, Vespa, PostgreSQL, Redis, Celery, or a real model server. For 95%+ enterprise-grade proof, run the same scenarios through the real deployed ingestion, vector retrieval, chat, and model-serving path in CI.
