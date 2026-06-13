> This is the client-facing mirror of the PHASE 13 prompt-injection review file. The canonical evidence copy remains under rag-security-readiness-review/02_evidence/phase_13/.

# Source Confusion Controls

## Source attribution checks
- Citation mappings are generated from tool responses and renumbered in chat output. `backend/onyx/chat/citation_utils.py:10-221`; `backend/onyx/chat/citation_processor.py:69-119,371+`.
- Source labels are displayed in the UI from `source_type` and `semantic_identifier`. `web/src/components/search/results/Citation.tsx:37-123`.

## Source metadata validation
- Metadata is preserved through search-doc construction and tool output formatting. `backend/onyx/tools/tool_implementations/utils.py:21-119`; `backend/onyx/context/search/context/search/models.py:235-246`.
- No explicit metadata authenticity check was identified.

## Connector source identity
- File IDs, document IDs, and semantic identifiers travel through the retrieval pipeline. `backend/onyx/context/search/utils.py:178-211`; `backend/onyx/context/search/context/search/models.py:235-246`.
- No source-only evidence showed a connector-identity verification step that would stop source spoofing.

## Metadata normalization
- Some text and filename sanitization exists during ingestion and serialization. `backend/onyx/utils/postgres_sanitization.py:15-49`; `backend/onyx/utils/text_processing.py:275-288`; `backend/onyx/context/search/utils.py:178-187`.
- Normalization is not the same as integrity validation.

## Answer-source alignment
- Citation ordering and mapping are maintained, but no source-only evidence showed alignment checking between answer claims and source content.

## Missing evidence
- No explicit answer-source mismatch detector.
- No runtime source-integrity validation.

## Unverified risks
- Document text can masquerade as authoritative source metadata if the content is crafted maliciously.
- Users may misread rendered citations or source labels as trust guarantees.
