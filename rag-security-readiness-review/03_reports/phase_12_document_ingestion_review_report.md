# PHASE 12 — Document Ingestion Security Review Report

## Executive summary

PHASE 12 completed a source-only document ingestion security review for the current checkout. The review traced how files, connector documents, parsed content, chunks, metadata, permissions, embeddings, indexes, updates, and deletions appear to move through the system at source level. It identified source-backed ingestion paths and separated confirmed findings, observations, and unverified risks.

Because PHASE 12 did not run tests, CI, exploit tests, live uploads, live connector syncs, live parser execution, live index checks, live database checks, live storage checks, or production validation, the status is **COMPLETE WITH LIMITATIONS**.

## Evidence basis

Evidence was drawn from previous PHASE 5, PHASE 8, PHASE 9, PHASE 10, and PHASE 11 files; source searches preserved in `rag-security-readiness-review/02_evidence/phase_12/raw_outputs/`; and source files under backend ingestion, upload, connector, file processing, indexing, document-index, database, background-task, frontend upload, and test directories.

## Upload entry point summary

User project uploads are source-visible in `backend/onyx/server/features/projects/api.py` L128-L167 and `backend/onyx/db/projects.py` L58-L178. Admin/file connector uploads and connector file updates are source-visible in `backend/onyx/server/documents/connector.py` L449-L566, L617-L623, and L693-L912. Frontend upload paths were identified in admin connector and project upload UI/client code. Runtime upload behavior was not validated.

## Connector ingestion entry point summary

Connector contracts are source-visible in `backend/onyx/connectors/interfaces.py` L117-L155 and L240-L329. File connector ingestion is source-visible in `backend/onyx/connectors/file/connector.py` L80-L367. Selected permission-aware connector paths were identified for Confluence and Google Drive. Runtime connector ingestion and connector permission correctness were not validated.

## File parsing summary

User upload validation and categorization are source-visible in `backend/onyx/server/features/projects/projects_file_utils.py` L39-L69 and L161-L393. Parser extension routing is source-visible in `backend/onyx/file_processing/extract_file_text.py` L721-L774 and multi-format extraction dispatch in L835-L931. ZIP handling exists in source paths. Runtime parser behavior for hostile or malformed files was not validated.

## Document chunking summary

Chunking is source-visible in `backend/onyx/indexing/chunker.py` L37-L67 and L120-L305, with section dispatch in `backend/onyx/indexing/chunking/document_chunker.py` L20-L114 and text chunking in `backend/onyx/indexing/chunking/text_section_chunker.py` L19-L117. Runtime chunk contents were not inspected.

## Metadata extraction summary

File, document, connector, document-set, and access metadata paths are source-visible in `backend/onyx/db/projects.py` L58-L137, `backend/onyx/document_index/document_metadata.py` L15-L40, `backend/onyx/db/document.py` L600-L743, and `backend/onyx/db/document_set.py` L241-L412. Metadata leakage and citation/source spoofing remain unverified.

## Indexing summary

Batch preparation and DB upsert are source-visible in `backend/onyx/indexing/indexing_pipeline.py` L494-L587. Document filtering is source-visible in L596-L693. The main chunk/embed/write pipeline is source-visible in L1240-L1425. Vespa and OpenSearch index update/delete paths were identified. Live index behavior was not validated.

## Embedding summary

Embedding input construction is source-visible in `backend/onyx/indexing/embedder.py` L118-L226, with model/settings construction in L228-L240. Source evidence indicates chunk text and selected metadata can be included in embedded content. Runtime provider configuration, request payloads, and retention behavior were not validated.

## Document update/delete summary

Source-level DB deletion and file cleanup paths exist in `backend/onyx/db/document.py` L900-L1036. Vespa index update/delete paths exist in `backend/onyx/document_index/vespa/vespa_document_index.py` L643-L847 and delete helper code in `backend/onyx/document_index/vespa/deletion.py` L17-L69. Live deletion/stale-index behavior was not validated.

## Permission sync during ingestion summary

Permission-aware connector contracts, selected connector permission-sync retrieval paths, permission-sync attempt DB helpers, access metadata persistence, and index metadata sync tasks were identified. Runtime permission-sync completeness/timing and retrieval ACL effects were not validated.

## Ingestion risk summary

PHASE 12 identified unverified risks for unsafe files, oversized documents, malicious parser inputs, prompt-injection documents, metadata leakage, source/citation spoofing, poisoned documents, stale permissions, deleted documents remaining indexed, connector over-indexing, sensitive text to embedding providers, parser DoS, and archive expansion.

## Ingestion test summary

Ingestion-related tests/evidence files were discovered by source search, including upload, parser, chunking, indexing, embedding, file-store, user-file processing, connector, permission-sync, and frontend upload tests. None were executed for PHASE 12, and no pass/fail results are claimed.

## Confirmed findings

5 confirmed source-level findings are documented in `rag-security-readiness-review/02_evidence/phase_12/ingestion_findings.md`.

## Observations

10 observations are documented in `rag-security-readiness-review/02_evidence/phase_12/ingestion_findings.md`.

## Unverified risks

13 unverified risks are documented in `rag-security-readiness-review/02_evidence/phase_12/ingestion_findings.md` and `rag-security-readiness-review/02_evidence/phase_12/ingestion_risks.md`.

## Missing evidence

Missing evidence includes runtime ingestion traces, executed tests, CI, production telemetry, live database rows, live vector/keyword index state, live connector state, live storage contents, embedding provider request evidence, malicious/oversized/archive negative-test evidence, and post-delete retrieval validation.

## Limitations

Source-only, current-checkout review. Runtime ingestion behavior, tests, CI, production behavior, live database state, live vector/keyword index state, live connector state, and live file/object storage state were not validated. Original-source and prior working-copy state remain unavailable.

## Non-claims

PHASE 12 does not claim ingestion controls are effective, tests passed, exploitability, production readiness, runtime ACL enforcement, live deletion completeness, live permission sync correctness, or absence of controls where no evidence was found.

## PHASE 12 status

**COMPLETE WITH LIMITATIONS**

## Exact next phase

PHASE 13 — Review prompt-injection exposure
