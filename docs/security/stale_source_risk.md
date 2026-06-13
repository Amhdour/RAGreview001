> This is the client-facing mirror of the PHASE 14 citation/source integrity review file. The canonical evidence copy remains under rag-security-readiness-review/02_evidence/phase_14/.


# Stale Source Risk

| Stale source path | File/path evidence | What is confirmed | What is unverified | Potential impact | Later validation method |
| ----------------- | ------------------ | ----------------- | ------------------ | ---------------- | ----------------------- |
| Deleted document source display | `backend/onyx/db/document.py`; `backend/onyx/server/query_and_chat/session_loading.py` | Document and session state can persist after indexing and deletion-related operations | Whether deleted documents are always removed from all source displays | Users may see sources that no longer exist | Test post-delete search/chat source rendering |
| Stale connector metadata | `backend/onyx/db/document.py`; `backend/onyx/connectors/web/connector.py` | Connector metadata can be updated and reindexed over time | Whether the UI always refreshes after connector changes | Outdated title or URL display | Validate connector update propagation |
| Stale index metadata | `backend/onyx/db/models.py`; `backend/onyx/document_index/opensearch/opensearch_document_index.py` | Indexing persists document metadata and content hashes | Whether index refresh always matches source-system state | Search may display stale source details | Run live reindex and refresh validation |
| Outdated title/URL | `backend/onyx/connectors/models.py`; `backend/onyx/context/search/models.py`; `web/src/components/search/results/Citation.tsx` | Title/URL fields are reused across multiple layers | Whether old labels are purged after source changes | Misleading citations or source cards | Compare updated source records to rendered labels |
| Cached chat/source history | `backend/onyx/server/query_and_chat/session_loading.py`; `backend/onyx/chat/llm_loop.py` | Historical chat packets can reconstruct sources later | Whether cached source records are refreshed after source deletion | Old source links may persist in chat history | Validate session reload after deletions |
| Post-delete source access | `backend/onyx/db/document.py`; `backend/onyx/db/document_set.py` | Deletion and access state are represented in backend tables | Whether access to deleted sources is blocked everywhere the UI exposes them | Inaccessible but visible source links | Test delete-and-render flows with authorization checks |
