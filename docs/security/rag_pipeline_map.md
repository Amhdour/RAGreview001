> This is the client-facing mirror of the PHASE 5 evidence file. The canonical evidence copy remains under rag-security-readiness-review/02_evidence/phase_5/.

# PHASE 5 RAG Pipeline Map

## 1. Purpose
This map identifies repository evidence for document ingestion, chunking, embedding, vector/search storage, retrieval, and chat/answer generation.

## 2. Scope
- In scope: `backend/onyx/connectors/`, `backend/onyx/indexing/`, `backend/onyx/document_index/`, `backend/onyx/server/documents/`, `backend/onyx/server/features/search/`, `backend/onyx/server/query_and_chat/`, `backend/onyx/chat/`, `backend/onyx/llm/`, and RAG-related DB modules under `backend/onyx/db/`.
- Out of scope: quality evaluation results, live connector credentials, live indexed corpus contents, and runtime vector database state.

## 3. Main entry points
- Connector interfaces and registry/factory: `backend/onyx/connectors/interfaces.py`, `backend/onyx/connectors/registry.py`, `backend/onyx/connectors/factory.py`, `backend/onyx/connectors/connector_runner.py`.
- Ingestion/admin APIs: `backend/onyx/server/documents/connector.py`, `backend/onyx/server/documents/credential.py`, `backend/onyx/server/documents/cc_pair.py`, `backend/onyx/server/onyx_api/ingestion.py`.
- Indexing pipeline: `backend/onyx/indexing/indexing_pipeline.py`.
- Chunking: `backend/onyx/indexing/chunker.py`, `backend/onyx/indexing/models.py`.
- Embedding: `backend/onyx/indexing/embedder.py`.
- Vector/index insertion: `backend/onyx/indexing/vector_db_insertion.py`, `backend/onyx/document_index/interfaces_new.py`, `backend/onyx/document_index/factory.py`.
- Retrieval/search API: `backend/onyx/server/features/search/api.py`, `backend/onyx/tools/tool_implementations/search/search_tool.py`.
- Chat/answer generation: `backend/onyx/server/query_and_chat/chat_backend.py`, `backend/onyx/chat/process_message.py`, `backend/onyx/chat/llm_loop.py`, `backend/onyx/chat/llm_step.py`, `backend/onyx/llm/factory.py`.
- RAG data models: `backend/onyx/db/models.py`, `backend/onyx/db/document.py`, `backend/onyx/db/chunk.py`, `backend/onyx/db/index_attempt.py`, `backend/onyx/db/search_settings.py`.

## 4. Architecture flow
1. Connector configuration and credentials are managed through document/admin route modules and persisted through DB helper/model files.
2. Connector code under `backend/onyx/connectors/` defines how external source documents are represented and fetched.
3. `backend/onyx/indexing/indexing_pipeline.py` prepares documents, updates DB document records, invokes chunking, invokes embedding, and writes chunks through vector insertion helpers.
4. `backend/onyx/indexing/chunker.py` and `backend/onyx/indexing/models.py` represent chunk construction and chunk-related data structures.
5. `backend/onyx/indexing/embedder.py` represents embedding logic used during indexing.
6. `backend/onyx/indexing/vector_db_insertion.py` and `backend/onyx/document_index/` represent the vector/search index insertion and abstraction layer.
7. `backend/onyx/server/features/search/api.py` constructs a search flow using persona/search filters, LLM selection, document index factory, and `SearchTool`.
8. Chat routes under `backend/onyx/server/query_and_chat/` and chat modules under `backend/onyx/chat/` represent answer-generation orchestration using LLM modules under `backend/onyx/llm/`.

## 5. Supporting evidence
- `backend/onyx/connectors/interfaces.py`, `backend/onyx/connectors/models.py`, `backend/onyx/connectors/factory.py`, `backend/onyx/connectors/registry.py` — connector framework evidence.
- `backend/onyx/server/documents/connector.py`, `backend/onyx/server/documents/credential.py`, `backend/onyx/server/documents/cc_pair.py`, `backend/onyx/server/onyx_api/ingestion.py` — ingestion/admin API evidence.
- `backend/onyx/indexing/indexing_pipeline.py` — pipeline imports and orchestration for document DB updates, chunking, embedding, contextual RAG, and vector insertion.
- `backend/onyx/indexing/chunker.py`, `backend/onyx/indexing/embedder.py`, `backend/onyx/indexing/vector_db_insertion.py` — chunking, embedding, and vector insertion evidence.
- `backend/onyx/document_index/interfaces_new.py`, `backend/onyx/document_index/factory.py`, `backend/onyx/document_index/vespa_constants.py` — document-index abstraction/factory and Vespa-related constants.
- `backend/onyx/server/features/search/api.py`, `backend/onyx/tools/tool_implementations/search/search_tool.py` — retrieval/search flow evidence.
- `backend/onyx/server/query_and_chat/chat_backend.py`, `backend/onyx/chat/process_message.py`, `backend/onyx/chat/llm_loop.py`, `backend/onyx/chat/llm_step.py` — chat generation orchestration evidence.
- `backend/onyx/llm/factory.py`, `backend/onyx/llm/interfaces.py` — LLM creation/abstraction evidence.

## 6. Dependencies
- Internal dependencies: connectors feed indexing; indexing uses DB helpers, chunking, embedding, and document-index insertion; search/chat use document index, tools, DB state, and LLM modules.
- External services/infrastructure supported by files: vector/search index represented by `backend/onyx/document_index/` and Vespa constants; external LLM providers represented by `backend/onyx/llm/`; relational DB represented by `backend/onyx/db/`.

## 7. Gaps / unknowns
- Live connector schedules, live credentials, corpus size, indexed document count, and vector index health are runtime data and not claimed.
- Retrieval quality and hallucination behavior are not evaluated by this architecture map.

## 8. Client-ready summary
The RAG architecture is organized as a pipeline: connectors bring in source documents, indexing code prepares and chunks them, embedding code converts chunks for search, document-index code stores/searches them, search APIs retrieve relevant content, and chat/LLM code uses retrieved context to generate responses.

## Support table
| Claim | Evidence file paths | Support status | Notes |
|---|---|---:|---|
| Connectors are a distinct ingestion layer. | `backend/onyx/connectors/interfaces.py`, `backend/onyx/connectors/factory.py`, `backend/onyx/connectors/registry.py` | Supported | Connector interfaces/factory/registry files exist. |
| Document/admin APIs manage connector and ingestion surfaces. | `backend/onyx/server/documents/connector.py`, `backend/onyx/server/documents/credential.py`, `backend/onyx/server/onyx_api/ingestion.py` | Supported | Route modules exist for connector, credential, and ingestion APIs. |
| Indexing includes chunking, embedding, and vector insertion modules. | `backend/onyx/indexing/indexing_pipeline.py`, `backend/onyx/indexing/chunker.py`, `backend/onyx/indexing/embedder.py`, `backend/onyx/indexing/vector_db_insertion.py` | Supported | Pipeline and stage-specific files exist. |
| The document index abstraction is separate from indexing pipeline code. | `backend/onyx/document_index/interfaces_new.py`, `backend/onyx/document_index/factory.py` | Supported | Interface and factory files are separate. |
| Retrieval/search routes connect to document index, LLM selection, and search tool code. | `backend/onyx/server/features/search/api.py`, `backend/onyx/tools/tool_implementations/search/search_tool.py`, `backend/onyx/llm/factory.py` | Supported | Search route imports and constructs these dependencies. |
| Chat/answer generation is represented by chat route and chat orchestration modules. | `backend/onyx/server/query_and_chat/chat_backend.py`, `backend/onyx/chat/process_message.py`, `backend/onyx/chat/llm_loop.py`, `backend/onyx/chat/llm_step.py` | Supported | Chat route and orchestration files exist. |
| Live indexed corpus quality is known. | No repository evidence identified. | Unsupported | Requires runtime data and evaluation. |

## Missing or unsupported items
- Live connector state, live index health, corpus size, retrieval quality, and answer quality are unsupported by repository files alone.
