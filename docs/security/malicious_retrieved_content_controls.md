> This is the client-facing mirror of the PHASE 13 prompt-injection review file. The canonical evidence copy remains under rag-security-readiness-review/02_evidence/phase_13/.

# Malicious Retrieved-Content Controls

## Detection of malicious instructions inside retrieved content
- No source-visible detector or classifier specifically for malicious instructions inside retrieved docs was identified.
- Retrieval and section classification exist, but they target relevance, not malicious instruction detection. `backend/onyx/secondary_llm_flows/document_filter.py:22-203`.

## Filtering unsafe chunks
- Search filters and ACL/doc-set filters reduce scope. `backend/onyx/context/search/pipeline.py:41-117`.
- No source-only evidence showed unsafe-chunk rejection based on content semantics.

## Demotion/quarantine/rejection behavior
- Re-ranking, deduplication, and section selection can demote items by relevance. `backend/onyx/tools/tool_implementations/search/search_utils.py:28-470`.
- No quarantine path for malicious prompt-injection content was identified.

## Post-retrieval scanning
- No post-retrieval prompt-injection scan or model-output scanner was identified in the reviewed sources.

## Missing runtime evidence
- No runtime tests, CI, or live RAG evidence were collected.

## Client-ready summary
The source review shows retrieval shaping and access filtering, but not a dedicated control that detects or quarantines malicious instructions inside retrieved content. This remains unverified.
