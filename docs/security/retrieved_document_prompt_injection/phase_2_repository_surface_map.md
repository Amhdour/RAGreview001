# PHASE 2 — Repository Surface Map

## Repository
`Amhdour/RAGreview001`

## Branch
`review/retrieved-doc-prompt-injection-phase-1`

## Baseline commit
`a56ed8ec60afc59de1b53ea83c23249424ec5fc3`

## Objective
Record the repository areas that are relevant to future review of retrieved document handling.

## Source evidence
- `docs/security/baseline_inventory.md`
- `docs/security/security_relevant_files.md`

## Mapped areas

| Area | Paths | Status |
| --- | --- | --- |
| Document ingestion | `backend/onyx/connectors/factory.py`; `backend/onyx/connectors/mock_connector/connector.py`; `backend/onyx/indexing/chunking/document_chunker.py`; `backend/onyx/file_processing/extract_file_text.py`; `backend/onyx/server/documents/document.py` | MAPPED |
| External document sync | `backend/ee/onyx/external_permissions/google_drive/doc_sync.py`; `backend/ee/onyx/external_permissions/sharepoint/doc_sync.py`; `backend/ee/onyx/external_permissions/slack/doc_sync.py`; `backend/ee/onyx/external_permissions/github/doc_sync.py` | CANDIDATE |
| Retrieval and indexing | `backend/onyx/document_index/vespa/chunk_retrieval.py`; `backend/onyx/document_index/vespa/vespa_document_index.py`; `backend/onyx/document_index/opensearch/search.py`; `backend/onyx/server/features/search/api.py` | MAPPED |
| Prompt and context handling | `backend/onyx/prompts/contextual_retrieval.py`; `backend/ee/onyx/prompts/query_expansion.py`; `backend/onyx/secondary_llm_flows/query_expansion.py`; `backend/onyx/chat/citation_processor.py` | MAPPED |
| Context shaping candidates | `backend/onyx/document_index/chunk_content_enrichment.py`; `backend/onyx/server/query_and_chat/chat_utils.py`; `backend/ee/onyx/server/query_and_chat/search_backend.py` | CANDIDATE |
| Citation and source display | `backend/onyx/chat/citation_processor.py`; `backend/onyx/chat/citation_utils.py`; `web/src/components/search/results/Citation.tsx`; `backend/onyx/document_index/vespa/chunk_retrieval.py` | MAPPED |
| Permissions | `backend/onyx/auth/permissions.py`; `backend/ee/onyx/external_permissions/google_drive/permission_retrieval.py`; `backend/ee/onyx/external_permissions/sharepoint/permission_utils.py`; `backend/ee/onyx/external_permissions/slack/channel_access.py` | MAPPED |
| Tool and action surfaces | `backend/onyx/coding_agent/mock_tools.py`; `backend/onyx/server/features/tool/api.py`; `backend/onyx/server/manage/code_interpreter/api.py`; `backend/onyx/server/manage/image_generation/api.py`; `web/src/app/admin/actions/page.tsx` | MAPPED |
| MCP and skill candidates | `.mcp.json`; `backend/onyx/mcp_server_main.py`; `backend/onyx/mcp_server/api.py`; `backend/onyx/server/features/skill/api.py`; `backend/onyx/server/features/mcp/api.py` | CANDIDATE |
| Logging and metrics | `backend/onyx/tracing/flows.py`; `backend/onyx/server/metrics/metrics_server.py`; `backend/ee/onyx/utils/telemetry.py` | MAPPED |
| Tests | `backend/tests/`; `web/tests/`; `backend/tests/integration/tests/security/test_runtime_security_settings.py` | MAPPED |

## Checklist

| Item | Status |
| --- | --- |
| Ingestion paths identified | COMPLETE |
| Chunking path identified | COMPLETE |
| Retrieval paths identified | COMPLETE |
| Prompt and context paths identified | COMPLETE |
| Citation paths identified | COMPLETE |
| Permission paths identified | COMPLETE |
| Tool/action paths identified | COMPLETE |
| Logging and metrics paths identified | COMPLETE |
| Test areas identified | COMPLETE |

## Limitations
- Source mapping only.
- No runtime execution.
- No tests run.
- No code behavior verified.
- Candidate paths require later validation.

## Phase result
PHASE 2 repository surface mapping is complete.
