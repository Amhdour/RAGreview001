> This is the client-facing mirror of the PHASE 13 prompt-injection review file. The canonical evidence copy remains under rag-security-readiness-review/02_evidence/phase_13/.

# Citation/Source Insertion

| Citation/source path | File/path | Line reference if available | Source data inserted/displayed | Validation/sanitization evidence | Spoofing relevance | Evidence label | Limitation |
| -------------------- | --------- | --------------------------- | ------------------------------ | -------------------------------- | ------------------ | -------------- | ---------- |
| Chat citation processor | backend/onyx/chat/citation_processor.py:69-119,371+; backend/onyx/chat/citation_utils.py:10-221; backend/onyx/tools/tool_runner.py:228-447; backend/onyx/tools/tool_implementations/utils.py:21-119 | chat/citation_processor.py:69-119,371+ | Citation numbers / markdown links | Citation mode controls and renumbering | Citation text is rendered into final answers | OBSERVATION | No anti-spoofing runtime proof |
| Citation mapping updates from tool output | backend/onyx/chat/citation_processor.py:69-119,371+; backend/onyx/chat/citation_utils.py:10-221; backend/onyx/tools/tool_runner.py:228-447; backend/onyx/tools/tool_implementations/utils.py:21-119 | citation_utils.py:10-221; tool_runner.py:228-447 | SearchDocsResponse citation metadata | Mapping merges and citation ordering | Tool responses can alter citation mappings | OBSERVATION | Source trust not verified at runtime |
| Tool response source metadata | backend/onyx/chat/citation_processor.py:69-119,371+; backend/onyx/chat/citation_utils.py:10-221; backend/onyx/tools/tool_runner.py:228-447; backend/onyx/tools/tool_implementations/utils.py:21-119 | tools/tool_implementations/utils.py:21-119 | title, url, document_identifier, file_name, metadata | Structured JSON-like output | Source metadata is preserved alongside content | OBSERVATION | Metadata integrity not proven |
| Frontend citation display | web/src/components/search/results/Citation.tsx:37-123 | UI renders source_type and semantic_identifier | Source label shown to users | Display/tooltip logic only | Source labels can be confusing if metadata is spoofed | OBSERVATION | UI display is not a validation layer |
| Document/source identity helpers | backend/onyx/chat/citation_processor.py:69-119,371+; backend/onyx/chat/citation_utils.py:10-221; backend/onyx/tools/tool_runner.py:228-447; backend/onyx/tools/tool_implementations/utils.py:21-119 | context/search/utils.py:178-211; context/search/models.py:235-246 | file_id, source, document identifiers | Filename and identifier helpers | Source identity is carried through retrieval paths | OBSERVATION | No explicit source-identity verification found |

## Notes
- Citation insertion is present in both chat output and tool output.
- The reviewed sources do not prove citation/source spoofing resistance.
