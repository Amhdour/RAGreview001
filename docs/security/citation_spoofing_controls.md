> This is the client-facing mirror of the PHASE 13 prompt-injection review file. The canonical evidence copy remains under rag-security-readiness-review/02_evidence/phase_13/.

# Citation Spoofing Controls

## Citation generation
- Citations are generated and renumbered across tool and chat flows. `backend/onyx/chat/citation_processor.py:69-119,371+`; `backend/onyx/chat/citation_utils.py:100-221`.

## Citation rendering
- Final answers may render citations as markdown links or numbered references. `backend/onyx/chat/citation_processor.py:69-119,371+`.
- The frontend citation component displays source labels and opens the corresponding document. `web/src/components/search/results/Citation.tsx:37-123`.

## Source title/URL sanitization
- Some sanitization occurs on stored text and filenames, but no citation-specific title/url validation was identified. `backend/onyx/utils/postgres_sanitization.py:15-49`; `backend/onyx/context/search/utils.py:178-187`.

## Prevention of document text pretending to be citation
- No source-only evidence showed a guard that detects document text mimicking citation syntax or source markup.

## Citation tests
- Existing unit tests cover citation extraction, collapse, and processor behavior, but they were not executed in this review. `backend/tests/unit/onyx/chat/test_citation_processor.py`; `backend/tests/unit/onyx/chat/test_citation_utils.py`.

## Missing evidence
- No runtime citation-spoofing validation.
- No dedicated anti-spoofing test execution evidence.

## Unverified risks
- Malicious content could imitate citation syntax or source labels.
- Rendered citation metadata may be trusted more than the underlying source warrants.
