
# Source Trust Assumptions

## Trusted source metadata assumptions
The code assumes `document_id`, `semantic_identifier`, `link`, `source_type`, and `metadata` describe the same source object across retrieval and display paths. See `backend/onyx/context/search/models.py:244-307` and `web/src/components/search/results/Citation.tsx:67-123`.

## Untrusted document content assumptions
Retrieved text can flow into citation-adjacent and source-adjacent structures, but this review found no source-only proof that the content itself is prevented from influencing labels or user interpretation. See `backend/onyx/chat/llm_loop.py:965-1074` and `web/src/refresh-components/buttons/source-tag/SourceTagDetailsCard.tsx:114-176`.

## Connector metadata trust assumptions
Connector-derived titles, URLs, and metadata are accepted and persisted through the ingestion pipeline. See `backend/onyx/connectors/web/connector.py:419-604` and `backend/onyx/db/document.py:667-716`.

## Source URL/title validation assumptions
Some normalization exists, but this review did not identify a citation-specific authenticity or canonicalization check. See `backend/onyx/connectors/web/connector.py:273-285` and `backend/onyx/file_processing/extract_file_text.py:153-210,310-361`.

## Access recheck assumptions
ACL and document-set state exist in the backend, but source display paths do not show a visible runtime authorization recheck before rendering. See `backend/onyx/access/models.py:174-227`, `backend/onyx/db/document_set.py:164-179,253-314`, and `web/src/components/search/results/Citation.tsx:75-123`.

## Stale metadata assumptions
Updated metadata can be stored, but the current checkout does not prove that all displayed source labels are refreshed after deletion or metadata changes. See `backend/onyx/db/document.py:706-736` and `backend/onyx/server/query_and_chat/session_loading.py:476-526,840-900`.

## Citation-to-authorized-result assumptions
Backend citation maps tie a citation number to a document ID, but the review did not validate that the final rendered source always corresponds to an authorized live retrieval result. See `backend/onyx/chat/citation_processor.py:215-247,484-531` and `backend/onyx/chat/llm_loop.py:650-1074`.

## Missing runtime evidence
No runtime source integrity evidence was collected for this phase.

## Client-ready summary
Source metadata is clearly propagated through backend and frontend layers, but the review cannot confirm that every displayed source label is authoritative, fresh, and access-checked at runtime.
