# Indirect Prompt-Injection Controls

## Uploaded document controls
- Uploaded and attached files can become context files and are serialized into chat prompt context. `backend/onyx/chat/llm_loop.py:570-602`.
- Text extraction and storage sanitization exist, but no source-only evidence showed malicious-instruction detection. `backend/onyx/file_processing/html_utils.py:27-223`; `backend/onyx/utils/postgres_sanitization.py:15-49`.

## Connector content controls
- Connector content enters the retrieval pipeline through indexed chunks and sections. `backend/onyx/document_index/vespa/indexing_utils.py:167-205`; `backend/onyx/document_index/opensearch/opensearch_document_index.py:196-214`.
- ACL and doc-set filters constrain retrieval scope. `backend/onyx/context/search/preprocessing/access_filters.py:8-21`; `backend/onyx/context/search/pipeline.py:41-117`.

## Retrieved content controls
- Retrieved content is ranked, expanded, and emitted as section text or JSON-like LLM output. `backend/onyx/tools/tool_implementations/search/search_utils.py:28-470`; `backend/onyx/tools/tool_implementations/utils.py:21-119`.
- No dedicated retrieved-context filter or scanner was identified.

## Source metadata controls
- Source identity fields such as title, URL, document identifier, and file name are preserved. `backend/onyx/tools/tool_implementations/utils.py:21-119`; `backend/onyx/context/search/context/search/models.py:235-246`.
- The reviewed sources do not show source-identity validation specifically for injection resistance.

## Cross-document instruction controls
- Deduplication, ranking, and section selection reduce context volume. `backend/onyx/tools/tool_implementations/search/search_utils.py:28-470`; `backend/onyx/secondary_llm_flows/document_filter.py:22-203`.
- No explicit cross-document instruction quarantine was identified.

## Missing evidence
- No runtime prompt-injection test evidence.
- No explicit detector, blocklist, or policy engine for indirect prompt injection.

## Unverified risks
- Malicious instructions embedded in retrieved or uploaded documents may reach LLM context.
- Source metadata could confuse answer trust boundaries.
- Cross-document contamination remains plausible where many chunks are merged.
