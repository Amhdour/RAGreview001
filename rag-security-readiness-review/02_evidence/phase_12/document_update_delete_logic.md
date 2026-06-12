# PHASE 12 — Document Update and Delete Logic

## Document update paths

- Source-level document DB upsert is implemented in `backend/onyx/db/document.py` L649-L743. It persists semantic ID, link, document timestamps, owners, external users/groups, public flag, document metadata, and file ID.
- Source-level document/index metadata sync is implemented by `document_index_metadata_sync_task` in `backend/onyx/background/celery/tasks/vespa/tasks.py` L460-L579. It builds metadata update requests from database access/document-set state and calls index update methods.
- Source-level OpenSearch update logic is implemented in `backend/onyx/document_index/opensearch/opensearch_document_index.py` L573-L650.
- Source-level Vespa update logic is implemented in `backend/onyx/document_index/vespa/vespa_document_index.py` L804-L847.

## Document deletion paths

- Source-level DB deletion is implemented in `delete_documents_complete__no_commit` in `backend/onyx/db/document.py` L900-L1036. It deletes related graph, chunk stats, connector relationships, feedback, tag, document rows, and then best-effort file records.
- Source-level delete-by-document helper is implemented in `backend/onyx/db/document.py` L1666-L1700.
- Source-level document-index delete contract is defined in `backend/onyx/document_index/interfaces_new.py` L205-L277.
- Source-level Vespa delete by document ID is implemented in `backend/onyx/document_index/vespa/vespa_document_index.py` L771-L802.

## Connector deletion sync

Connector deletion task code in `backend/onyx/background/celery/tasks/connector_deletion/tasks.py` L426-L539 removes index attempts, permission-sync attempts, document-set relationships, user-group relationships, orphan tags, documents for connector/credential pair, and connector-pair metadata in source code.

## Index deletion sync

Vespa chunk deletion helper code in `backend/onyx/document_index/vespa/deletion.py` L17-L69 issues retry-wrapped HTTP delete requests. This confirms a source-level delete helper but does not prove live index deletion completed.

## Chunk deletion sync

Vespa indexing code in `backend/onyx/document_index/vespa/vespa_document_index.py` L643-L769 computes old/new chunk-count ranges and deletes old chunks when new indexing produces fewer chunks. This is source-level chunk cleanup logic only.

## Soft-delete flags

Source search identified `DELETING` connector-pair filtering in access helper logic (`backend/onyx/db/document.py` L600-L646). A complete soft-delete state-machine review was not performed in PHASE 12 and remains unverified beyond cited paths.

## Hard-delete behavior if present

`delete_documents_complete__no_commit` directly deletes multiple database rows and then attempts best-effort file deletion (`backend/onyx/db/document.py` L900-L1036). Live database/object-storage deletion completeness was not validated.

## Stale document risks

Stale-document risk remains UNVERIFIED because source-level DB/index deletion paths do not prove runtime execution order, retry completion, or live vector/keyword index state. PHASE 11 also retained source-only stale/deleted-document limitations.

## Stale chunk risks

Stale chunk risk remains UNVERIFIED because source-level old-chunk deletion ranges and index delete helpers were not verified against live index state after document updates/deletes.

## Missing runtime evidence

Missing evidence includes runtime connector deletion traces, prune execution logs, live DB rows, live vector index state, live keyword index state, live object-storage contents, failed-delete retry outcomes, and post-delete retrieval checks.

## Client-ready summary

The current checkout contains source-level paths for document updates, database deletion, connector deletion cleanup, index metadata updates, and Vespa/OpenSearch index operations. PHASE 12 does not validate that these paths execute successfully in production or that deleted/stale documents are absent from live indexes.
