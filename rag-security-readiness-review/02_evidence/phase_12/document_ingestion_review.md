# PHASE 12 — Document Ingestion Security Review

## Scope

This PHASE 12 package reviews document ingestion security at source level only. It traces upload ingestion, connector ingestion, parser routing, chunking, metadata propagation, embedding input construction, indexing/update/delete paths, and permission-sync interactions in the current checkout.

The review covers source files and previous phase evidence only. It does not validate runtime behavior, production behavior, live database rows, live object storage, live connector state, live vector/keyword index state, CI, or test execution.

## Evidence basis

- Previous phase evidence: PHASE 10 control gaps, PHASE 8 ingestion risk-to-code mapping, PHASE 9 ingestion test/evidence mapping, PHASE 11 retrieval ACL/stale-document evidence, and PHASE 5 architecture evidence.
- Current-checkout source paths including backend upload APIs, file processing, connector interfaces, connector file ingestion, indexing pipeline, document-index implementations, database document/document-set/permission-sync helpers, background ingestion tasks, frontend upload UI/client paths, and tests discovered by source search.
- Raw search outputs are preserved in `rag-security-readiness-review/02_evidence/phase_12/raw_outputs/`.

## Document ingestion review method

1. Started from PHASE 10 ingestion/control gaps and PHASE 8 ingestion risk-to-code mapping.
2. Read PHASE 9 ingestion test/evidence mapping.
3. Read PHASE 11 retrieval ACL review for stale/deleted document and permission-sync implications.
4. Read PHASE 5 RAG pipeline and data model evidence.
5. Identified upload entry points.
6. Identified connector ingestion entry points.
7. Identified file parsing logic.
8. Identified document chunking logic.
9. Identified metadata extraction logic.
10. Identified indexing logic.
11. Identified embedding logic.
12. Identified document update and deletion logic.
13. Identified permission sync during ingestion.
14. Identified unsafe-file, oversized-document, metadata leakage, malicious-document, stale-document, deleted-document, poisoning, and permission-drift risks.
15. Identified ingestion-related tests and evidence files by source search only.
16. Separated confirmed findings, observations, and unverified risks.
17. Recorded missing runtime, test, CI, production, live connector, live index, and live storage evidence.

## Ingestion areas reviewed

- Upload entry points: user file upload, admin/file connector upload, connector file update, avatar upload, frontend file upload UI/client helpers.
- Connector ingestion: connector interfaces, connector runner, file connector, permission-aware connector interfaces, selected connector permission-sync implementations.
- Parsing: user-upload validation, password-protected-file checks, extension routing, text extraction, ZIP handling, MIME guessing.
- Chunking: section chunking, text chunking, metadata suffixing, chunk payloads, chunk overlap.
- Metadata: file metadata, connector metadata, document metadata, owner/access metadata, document-set metadata, source URL/title/citation-style metadata.
- Indexing: batch preparation, DB upsert, chunking, embedding, vector DB write, Vespa/OpenSearch update/delete logic.
- Embedding: embedder input construction, model selection from search settings, text/metadata inclusion in embedded content.
- Update/delete: DB document/file cleanup, staged-file promotion/deletion, document-set sync, connector deletion and pruning tasks, vector-index delete/update interfaces.
- Permission sync: permission-aware connector contracts, permission-sync attempt state, document access metadata, metadata sync to indexes, relationship to PHASE 11 retrieval ACL filters.

## Confirmed findings summary

- F-12-01 — User file uploads have a source-level route to indexed user-file processing and source-level validation code paths, but runtime enforcement was not validated.
- F-12-02 — Admin/file-connector upload paths include source-level ZIP expansion and file-store persistence paths, but archive-expansion safety and runtime limits were not validated.
- F-12-03 — Source-level parsing routes by extension and handles selected PDF/Office/HTML/text formats, but parser sandboxing and malicious-document behavior were not validated.
- F-12-04 — Source-level chunking and embedding paths can include document text plus selected metadata in content sent to the embedder, but provider-side behavior was not validated.
- F-12-05 — Source-level DB/index update and delete paths exist, but live index/database deletion completeness was not validated.

## Observations summary

- Upload ingestion and connector ingestion are separate paths and should not be treated as one control surface.
- User-file uploads perform pre-index validation before queuing Celery processing in source code.
- Connector file upload uses a separate admin/file-connector route and a file-store abstraction.
- File parsing, chunking, indexing, and embedding are distinct layers.
- The indexing pipeline sanitizes and persists documents, promotes staged files, chunks sections, embeds chunks, and writes chunks to a document index in source code.
- DB document upsert code preserves existing external-access values during non-permission indexing updates.
- Vespa and OpenSearch index implementations expose source-level update/delete code paths.
- Permission-sync state is represented in database helper code and connector interfaces.
- Existing ingestion-related tests were discovered, but were not executed for PHASE 12.
- Prior PHASE 11 evidence remains relevant for stale/deleted document and ACL-filter implications.

## Unverified risks summary

The following remain unverified because runtime/test/production/live evidence was unavailable: unsafe file ingestion, oversized document bypass, malicious-document parser behavior, prompt-injection document ingestion, metadata leakage, source/citation spoofing through metadata, poisoned document indexing, stale permission ingestion, deleted documents remaining indexed, connector over-indexing, sensitive text sent to an external embedding provider, parser crash/DoS behavior, and archive/file expansion behavior.

## Missing evidence

- Runtime upload ingestion traces.
- Runtime parser behavior for malicious, malformed, oversized, encrypted, and archive inputs.
- Runtime connector ingestion and connector permission-sync evidence.
- Live database document/access/file-record state.
- Live vector and keyword index state after update/delete operations.
- Live object/file storage contents.
- Embedding provider request logs and provider-retention configuration.
- Executed ingestion test results.
- CI evidence.
- Production configuration and telemetry evidence.

## Limitations

Source-only, current-checkout review. Runtime ingestion behavior, tests, CI, production behavior, live database state, live vector/keyword index state, live connector state, and live file/object storage state were not validated. Original-source and prior working-copy state remain unavailable.

## Non-claims

- This review does not claim ingestion controls are effective in runtime or production.
- This review does not claim any ingestion test passed.
- This review does not claim exploitability.
- This review does not claim production readiness.
- This review does not prove absence of controls where evidence was not found.
- This review distinguishes source-level logic from runtime enforcement.

## Client-ready summary

PHASE 12 completed a source-only document ingestion security review for the current checkout. The review identified key upload, connector ingestion, parsing, chunking, metadata, embedding, indexing, update/delete, and permission-sync source paths and separated source-confirmed behavior from unverified runtime risks. Because runtime ingestion, tests, CI, live storage, live database state, live indexes, live connectors, and production behavior were not validated, PHASE 12 is **COMPLETE WITH LIMITATIONS**.
