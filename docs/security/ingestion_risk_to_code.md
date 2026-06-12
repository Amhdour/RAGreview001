> This is the client-facing mirror of the PHASE 8 evidence file. The canonical evidence copy remains under rag-security-readiness-review/02_evidence/phase_8/.

# Ingestion Risk to Code

## Category purpose
Map document upload, parsing, chunking, indexing, embedding, sync, and metadata paths that can admit or transform content before retrieval.

## Related PHASE 7 risks
- RAG-03
- RAG-05
- PI-01
- CONN-04
- CONN-05

## Related PHASE 6 threats
- TH-05
- TH-06
- TH-07
- TH-09

## Related PHASE 5 architecture evidence
- rag-security-readiness-review/02_evidence/phase_5/rag_pipeline_map.md
- rag-security-readiness-review/02_evidence/phase_5/backend_architecture.md
- rag-security-readiness-review/02_evidence/phase_5/data_model_map.md
- rag-security-readiness-review/02_evidence/phase_5/api_routes_map.md

## Related PHASE 3 inventory evidence
- rag-security-readiness-review/02_evidence/phase_3/baseline_inventory.md
- rag-security-readiness-review/02_evidence/phase_3/important_files_index.md
- rag-security-readiness-review/02_evidence/phase_3/security_relevant_files.md

## Candidate Onyx file paths
- backend/onyx/connectors/factory.py
- backend/onyx/connectors/connector_runner.py
- backend/onyx/document_index/vespa/indexing_utils.py
- backend/onyx/document_index/vespa/vespa_document_index.py
- backend/onyx/document_index/chunk_content_enrichment.py
- backend/onyx/document_index/document_metadata.py
- backend/onyx/file_processing/extract_file_text.py
- backend/onyx/file_processing/file_types.py
- backend/onyx/file_processing/unstructured.py
- backend/onyx/server/documents/document.py

## Existing control candidates
- ING-MAP-01: connector and indexing boundaries appear available.
- ING-MAP-02: file parsing and chunk-enrichment paths appear available.

## Missing control candidates
- No dedicated upload-path sanitization evidence was identified.

## Unverified mappings
- Ingestion controls are source-backed only and remain untested.

## Later validation methods
- Index-write validation.
- Parser robustness review.
- Malicious document path handling validation.

## Non-claims
- No claim that uploaded content is safe.
- No claim that chunking or indexing is resistant to malicious input.

## Client-ready summary
The ingestion surface spans connector instantiation, parsing, chunking, and index writes, but the current pass only identifies likely control points.

## Mapping table

| Mapping ID | Related risk ID/category | Related PHASE 6 threat ID | Related PHASE 5 architecture evidence | Candidate Onyx file/path | Mapping label | Why this file/path matters | Missing evidence | Later validation method | Notes |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| ING-MAP-01 | RAG-05 / CONN-05 | TH-06 / TH-09 | rag_pipeline_map.md; backend_architecture.md; data_model_map.md; api_routes_map.md | backend/onyx/connectors/factory.py; backend/onyx/connectors/connector_runner.py; backend/onyx/document_index/vespa/indexing_utils.py; backend/onyx/document_index/vespa/vespa_document_index.py | EXISTING-CANDIDATE | These files appear to govern connector instantiation, ingestion flow, and indexing into the search backend. | No live ingestion pipeline or index-write validation was performed. | Ingestion scope and sync-policy validation. | Source-level candidate for ingestion boundaries. |
| ING-MAP-02 | RAG-03 / PI-01 | TH-07 / TH-09 | rag_pipeline_map.md; backend_architecture.md; data_model_map.md; api_routes_map.md | backend/onyx/file_processing/extract_file_text.py; backend/onyx/file_processing/file_types.py; backend/onyx/file_processing/unstructured.py; backend/onyx/document_index/chunk_content_enrichment.py | EXISTING-CANDIDATE | These files suggest the file-parsing and chunk-enrichment boundary where malicious document content first becomes model-visible text. | No parser hardening or malicious document-path test was run. | Parser robustness and chunking review. | Relevant to ingestion of poisoned content. |
| ING-MAP-03 | RAG-05 | TH-09 | rag_pipeline_map.md; backend_architecture.md; data_model_map.md | backend/onyx/file_processing/extract_file_text.py | MISSING-CANDIDATE | A dedicated malicious-path normalization or upload-safety control path was not clearly identified beyond the general extraction code. | No dedicated path-sanitization or malicious-upload control evidence was found in this pass. | File-path validation and upload-safety review. | Gap in evidence, not proof of absence. |
