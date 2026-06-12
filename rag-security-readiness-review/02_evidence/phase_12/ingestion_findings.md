# PHASE 12 — Ingestion Findings

## Confirmed findings

### F-12-01 — User file upload routes into indexed user-file processing

- **Status:** CONFIRMED-FINDING.
- **Evidence:** `backend/onyx/server/features/projects/api.py` L128-L167; `backend/onyx/db/projects.py` L58-L178.
- **What is confirmed:** Source code defines a user project file upload endpoint, persists uploaded files as user files, and enqueues user-file indexing tasks with an expiration.
- **What is not confirmed:** Runtime auth enforcement, successful task execution, indexing results, and retrieval behavior were not validated.
- **Security relevance:** User-uploaded files are an ingestion entry point into searchable content.
- **Client-ready wording:** The source code contains a user-file ingestion path; PHASE 12 did not validate that the path behaves securely at runtime.

### F-12-02 — Connector file upload supports ZIP expansion and file-store persistence

- **Status:** CONFIRMED-FINDING.
- **Evidence:** `backend/onyx/server/documents/connector.py` L449-L566 and L617-L623.
- **What is confirmed:** Source code supports connector file uploads, optional ZIP expansion, MIME guessing, DOCX text conversion in one path, and file-store persistence.
- **What is not confirmed:** Archive expansion limits, malicious archive behavior, runtime authorization, and index results were not validated.
- **Security relevance:** Archive expansion and admin-managed file uploads are ingestion attack-surface areas.
- **Client-ready wording:** The source code supports connector file ingestion, including ZIP handling, but PHASE 12 did not test archive-safety behavior.

### F-12-03 — User file parsing has source-level validation and extension routing

- **Status:** CONFIRMED-FINDING.
- **Evidence:** `backend/onyx/server/features/projects/projects_file_utils.py` L161-L393; `backend/onyx/file_processing/extract_file_text.py` L721-L774.
- **What is confirmed:** Source code includes upload categorization, size checks, password-protected-file checks, extraction failure handling, and extension-based parser routing.
- **What is not confirmed:** Runtime parser resilience, malicious-document handling, parser sandboxing, and production config values were not validated.
- **Security relevance:** Parser and validation behavior determine which uploaded files can become indexed content.
- **Client-ready wording:** Source-level validation and routing exist, but PHASE 12 does not prove parser defenses are effective against hostile files.

### F-12-04 — Chunk text and selected metadata can enter embedding input

- **Status:** CONFIRMED-FINDING.
- **Evidence:** `backend/onyx/indexing/chunker.py` L37-L67 and L120-L305; `backend/onyx/indexing/embedder.py` L118-L226.
- **What is confirmed:** Source code can append selected metadata to chunk content and sends enriched chunk text to the embedding model.
- **What is not confirmed:** Runtime provider, provider retention, actual metadata values, and redaction behavior were not validated.
- **Security relevance:** Sensitive document text or metadata may be included in embedding requests depending on configuration and content.
- **Client-ready wording:** Source evidence shows embedding inputs may include document text plus selected metadata; runtime provider exposure remains unverified.

### F-12-05 — Source-level document and index update/delete paths exist but live cleanup is unverified

- **Status:** CONFIRMED-FINDING.
- **Evidence:** `backend/onyx/db/document.py` L900-L1036; `backend/onyx/document_index/vespa/vespa_document_index.py` L643-L847; `backend/onyx/document_index/vespa/deletion.py` L17-L69.
- **What is confirmed:** Source code includes DB document deletion, file cleanup, Vespa chunk update/delete behavior, and retry-wrapped chunk deletion helpers.
- **What is not confirmed:** Live DB rows, live file storage, live vector/keyword index state, and post-delete retrieval behavior were not validated.
- **Security relevance:** Incomplete runtime deletion could leave stale content available through search/retrieval.
- **Client-ready wording:** Cleanup paths exist in source, but PHASE 12 does not prove live deletion completeness.

## Observations

### O-12-01 — Upload ingestion and connector ingestion are separate paths

- **Status:** OBSERVATION.
- **Evidence:** User upload endpoint in `backend/onyx/server/features/projects/api.py` L128-L167; connector upload endpoint in `backend/onyx/server/documents/connector.py` L617-L623.
- **Meaning:** Upload ingestion should be reviewed separately for user files and connector files.
- **Limitation:** Runtime behavior was not validated.

### O-12-02 — Connector interfaces support permission-aware variants

- **Status:** OBSERVATION.
- **Evidence:** `backend/onyx/connectors/interfaces.py` L117-L155 and L240-L329.
- **Meaning:** Source-level connector contracts distinguish ordinary connector loading from permission-aware/checkpointed sync behavior.
- **Limitation:** Connector-specific runtime permissions were not validated.

### O-12-03 — File connector converts stored file records into `Document` objects

- **Status:** OBSERVATION.
- **Evidence:** `backend/onyx/connectors/file/connector.py` L80-L273.
- **Meaning:** Uploaded/stored file records can become connector documents.
- **Limitation:** Runtime file-store contents were not inspected.

### O-12-04 — Chunking is distinct from parsing and indexing

- **Status:** OBSERVATION.
- **Evidence:** `backend/onyx/indexing/chunking/document_chunker.py` L20-L114; `backend/onyx/indexing/indexing_pipeline.py` L1240-L1425.
- **Meaning:** Parsed sections are chunked before embedding and index writes.
- **Limitation:** Runtime chunk output was not inspected.

### O-12-05 — Document access metadata is persisted in DB source paths

- **Status:** OBSERVATION.
- **Evidence:** `backend/onyx/db/document.py` L600-L743.
- **Meaning:** Public/user/group access fields are part of source-level document metadata persistence.
- **Limitation:** Live ACL rows were unavailable.

### O-12-06 — Index implementations expose update/delete paths

- **Status:** OBSERVATION.
- **Evidence:** `backend/onyx/document_index/vespa/vespa_document_index.py` L643-L847; `backend/onyx/document_index/opensearch/opensearch_document_index.py` L573-L650.
- **Meaning:** Vespa and OpenSearch have source-level update/delete behavior.
- **Limitation:** Live index state was unavailable.

### O-12-07 — Permission-sync attempt state is modeled in DB helpers

- **Status:** OBSERVATION.
- **Evidence:** `backend/onyx/db/permission_sync_attempt.py` L36-L245.
- **Meaning:** Permission sync has source-level state tracking.
- **Limitation:** Runtime sync attempts were not inspected.

### O-12-08 — Frontend upload UI/client code exists

- **Status:** OBSERVATION.
- **Evidence:** `web/src/components/admin/connectors/FileUpload.tsx` L15-L52; `web/src/lib/fileConnector.ts` L18-L49; `web/src/providers/ProjectsContext.tsx` L489-L513.
- **Meaning:** Browser-facing paths initiate uploads into backend routes.
- **Limitation:** Browser/runtime behavior was not exercised.

### O-12-09 — Ingestion-related tests exist in source tree

- **Status:** OBSERVATION.
- **Evidence:** `rag-security-readiness-review/02_evidence/phase_12/raw_outputs/ingestion_tests_search_raw.txt`.
- **Meaning:** Test files were discovered for upload, parsing, chunking, indexing, embedding, file store, user-file processing, connector ingestion, and permission sync.
- **Limitation:** Tests were not run and no pass/fail result is claimed.

### O-12-10 — Prior PHASE 11 stale/deleted limitations still apply

- **Status:** OBSERVATION.
- **Evidence:** `rag-security-readiness-review/02_evidence/phase_11/deleted_stale_document_handling.md`.
- **Meaning:** Retrieval ACL and stale/deleted document behavior remains source-only unless later runtime validation is performed.
- **Limitation:** PHASE 12 did not perform retrieval or live index checks.

## Unverified risks

### UR-12-01 — Unsafe file ingestion

- **Status:** UNVERIFIED-RISK.
- **Why unverified:** Source validation/parsing paths exist, but runtime malicious-file behavior was not tested.
- **Missing evidence:** Malicious-file runtime tests, parser sandbox evidence, parser crash telemetry.
- **Later validation method:** Controlled negative parser/upload tests in an isolated environment.
- **Client-ready wording:** Unsafe-file handling remains a runtime validation item.

### UR-12-02 — Oversized document bypass

- **Status:** UNVERIFIED-RISK.
- **Why unverified:** Source size checks exist, but runtime configuration and bypass resistance were not validated.
- **Missing evidence:** Executed oversized-upload and oversized-index tests.
- **Later validation method:** Runtime limit tests with representative configs.
- **Client-ready wording:** Oversized-document control effectiveness is unproven by source review alone.

### UR-12-03 — Malicious document parser behavior

- **Status:** UNVERIFIED-RISK.
- **Why unverified:** Parser dispatch is source-visible, but malicious files were not executed.
- **Missing evidence:** Isolated parser robustness tests.
- **Later validation method:** Negative tests with malformed PDF/Office/HTML files.
- **Client-ready wording:** Parser resilience remains unverified.

### UR-12-04 — Prompt-injection document ingestion

- **Status:** UNVERIFIED-RISK.
- **Why unverified:** Text can become chunk content, but prompt-injection exposure is not validated here.
- **Missing evidence:** Prompt-injection ingestion/retrieval/generation tests.
- **Later validation method:** PHASE 13 prompt-injection review.
- **Client-ready wording:** Prompt-injection exposure is the next review focus.

### UR-12-05 — Metadata leakage

- **Status:** UNVERIFIED-RISK.
- **Why unverified:** Metadata suffixing exists, but actual runtime metadata values and exposures were not inspected.
- **Missing evidence:** Runtime chunk/embedding payload inspection.
- **Later validation method:** Controlled metadata fixture ingestion and request capture.
- **Client-ready wording:** Metadata exposure remains source-plausible but unproven.

### UR-12-06 — Source/citation spoofing through metadata

- **Status:** UNVERIFIED-RISK.
- **Why unverified:** Link/title/source metadata paths exist, but spoofing resistance was not validated.
- **Missing evidence:** Tests with adversarial metadata and UI/retrieval inspection.
- **Later validation method:** Connector/upload metadata validation tests.
- **Client-ready wording:** Citation/source spoofing requires targeted validation.

### UR-12-07 — Poisoned document indexing

- **Status:** UNVERIFIED-RISK.
- **Why unverified:** Indexing writes admitted chunks, but trust/ranking/poison-resistance was not tested.
- **Missing evidence:** Poisoning test cases and ranking analysis.
- **Later validation method:** Controlled poisoned corpus tests.
- **Client-ready wording:** Poisoned-content handling remains unverified.

### UR-12-08 — Stale permission ingestion

- **Status:** UNVERIFIED-RISK.
- **Why unverified:** Permission sync paths exist, but timing/completeness was not validated.
- **Missing evidence:** Live permission-change tests and index metadata inspection.
- **Later validation method:** Integration tests changing source permissions and checking retrieval.
- **Client-ready wording:** Permission drift remains a runtime validation requirement.

### UR-12-09 — Deleted document remaining indexed

- **Status:** UNVERIFIED-RISK.
- **Why unverified:** Delete paths exist, but live DB/index state was unavailable.
- **Missing evidence:** Post-delete live index checks and retrieval checks.
- **Later validation method:** Delete document, inspect DB/index, perform retrieval tests.
- **Client-ready wording:** Source-level deletion paths do not prove live cleanup.

### UR-12-10 — Connector over-indexing

- **Status:** UNVERIFIED-RISK.
- **Why unverified:** Connector scope and live permissions were not tested.
- **Missing evidence:** Connector fixture accounts and source-system scope verification.
- **Later validation method:** Connector-specific integration tests.
- **Client-ready wording:** Connector scope needs runtime validation.

### UR-12-11 — Sensitive text sent to embedding provider

- **Status:** UNVERIFIED-RISK.
- **Why unverified:** Embedding input construction is source-visible, but provider/config/request logs are unavailable.
- **Missing evidence:** Provider configuration, retention policy, and request payload inspection.
- **Later validation method:** Runtime config review and controlled embedding call tracing.
- **Client-ready wording:** Embedding-provider exposure remains unverified.

### UR-12-12 — Parser crash/DoS risk

- **Status:** UNVERIFIED-RISK.
- **Why unverified:** Parser failure handling exists, but stress/fuzz behavior was not tested.
- **Missing evidence:** Parser crash/timeout tests and worker telemetry.
- **Later validation method:** Isolated parser stress tests.
- **Client-ready wording:** Parser DoS resilience requires testing.

### UR-12-13 — Archive/file expansion risk

- **Status:** UNVERIFIED-RISK.
- **Why unverified:** ZIP handling exists, but expansion limits were not validated.
- **Missing evidence:** Archive-size/count/depth tests.
- **Later validation method:** Controlled archive expansion tests in a safe environment.
- **Client-ready wording:** Archive expansion needs runtime safety validation.

## No-evidence-found areas

- No executed PHASE 12 tests.
- No CI evidence.
- No production evidence.
- No live database evidence.
- No live vector or keyword index evidence.
- No live connector state evidence.
- No live file/object storage evidence.
- No confirmed public/shared anonymous document upload path in this pass.
- No confirmed malicious-document, zip-bomb, poisoning, or prompt-injection ingestion test execution evidence.
