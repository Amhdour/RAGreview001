> This is the client-facing mirror of the PHASE 13 prompt-injection review file. The canonical evidence copy remains under rag-security-readiness-review/02_evidence/phase_13/.

# Document Text Sanitization

| Sanitization/control path | File/path | Line reference if available | Input cleaned | Cleaning/control behavior | Missing evidence | Evidence label |
| ------------------------- | --------- | --------------------------- | ------------- | ------------------------- | ---------------- | -------------- |
| String sanitization helper | backend/onyx/utils/postgres_sanitization.py:15-49; backend/onyx/utils/text_processing.py:275-288; backend/onyx/document_index/vespa/indexing_utils.py:167-205; backend/onyx/document_index/opensearch/opensearch_document_index.py:196-214; backend/onyx/file_processing/html_utils.py:27-223 | utils/postgres_sanitization.py:15-49 | Strings / JSON-like values | Removes NUL bytes and invalid surrogates | No prompt-injection detection logic | OBSERVATION |
| Unicode cleanup | backend/onyx/utils/postgres_sanitization.py:15-49; backend/onyx/utils/text_processing.py:275-288; backend/onyx/document_index/vespa/indexing_utils.py:167-205; backend/onyx/document_index/opensearch/opensearch_document_index.py:196-214; backend/onyx/file_processing/html_utils.py:27-223 | utils/text_processing.py:275-288 | Extracted text | Removes invalid unicode / image markdown artifacts | Not a security sanitizer | OBSERVATION |
| HTML cleanup on ingestion | backend/onyx/utils/postgres_sanitization.py:15-49; backend/onyx/utils/text_processing.py:275-288; backend/onyx/document_index/vespa/indexing_utils.py:167-205; backend/onyx/document_index/opensearch/opensearch_document_index.py:196-214; backend/onyx/file_processing/html_utils.py:27-223 | file_processing/html_utils.py:27-223 | HTML documents | Strips some tags/classes and normalizes text | No prompt-injection filter found | OBSERVATION |
| Vespa indexing sanitization | backend/onyx/utils/postgres_sanitization.py:15-49; backend/onyx/utils/text_processing.py:275-288; backend/onyx/document_index/vespa/indexing_utils.py:167-205; backend/onyx/document_index/opensearch/opensearch_document_index.py:196-214; backend/onyx/file_processing/html_utils.py:27-223 | document_index/vespa/indexing_utils.py:167-205 | Metadata, blurbs, titles, content | Sanitizes content before indexing | Index sanitization does not prove prompt sanitization | OBSERVATION |
| OpenSearch indexing sanitization | backend/onyx/utils/postgres_sanitization.py:15-49; backend/onyx/utils/text_processing.py:275-288; backend/onyx/document_index/vespa/indexing_utils.py:167-205; backend/onyx/document_index/opensearch/opensearch_document_index.py:196-214; backend/onyx/file_processing/html_utils.py:27-223 | document_index/opensearch/opensearch_document_index.py:196-214 | Metadata, blurbs, titles, content | Applies unicode cleanup before storage | Not a prompt-injection control | OBSERVATION |

## Missing evidence
- No post-retrieval malicious-instruction stripper was identified.
- No prompt-injection-specific redaction or detector was identified.

## Notes
- Sanitization is present mainly for storage and text normalization.
- This evidence does not prove unsafe document text is removed before prompt insertion.
