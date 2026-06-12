> This is the client-facing mirror of the PHASE 12 document ingestion review file. The canonical evidence copy remains under rag-security-readiness-review/02_evidence/phase_12/.

# PHASE 12 — Document Chunking Logic

| Chunking path | File/path | Line reference if available | Input | Output | Metadata carried | Security relevance | Evidence label |
| ------------- | --------- | --------------------------- | ----- | ------ | ---------------- | ------------------ | -------------- |
| Chunker construction | `backend/onyx/indexing/chunker.py` | L120-L305 | `Document`, source, tenant/index context | `DocAwareChunk` and optional large chunks | Title prefix and metadata suffix can be attached to chunk content. | Metadata and document text can be propagated into indexed and embedded content. | CONFIRMED-FINDING |
| Metadata suffix generation | `backend/onyx/indexing/chunker.py` | L37-L67 | Document metadata dict | Human-readable metadata suffix | Metadata keys not ignored can be added to chunk text. | Metadata leakage/source spoofing concerns depend on metadata contents and downstream use. | OBSERVATION |
| Section-to-chunk dispatch | `backend/onyx/indexing/chunking/document_chunker.py` | L20-L114 | Text, image, and tabular document sections | Section-specific chunks and payloads | Payloads and section links can carry content references. | Distinguishes parsing output from chunking output. | OBSERVATION |
| Text section chunking | `backend/onyx/indexing/chunking/text_section_chunker.py` | L19-L117 | Text sections | Cleaned, split text chunks | Text content and link metadata may be carried. | Unsafe or prompt-injection text can become chunk content unless later controls apply. | UNVERIFIED-RISK |
| Chunk model metadata | `backend/onyx/indexing/models.py` | L49-L123 | Chunk/document metadata | `IndexChunk`/`DocMetadataAwareIndexChunk` fields | Access info, document sets, user projects, personas, boost, and hierarchy IDs can accompany chunks. | Permission metadata propagation is source-visible, but runtime enforcement is not proven. | OBSERVATION |
| Chunk update/delete handling | `backend/onyx/document_index/vespa/vespa_document_index.py` | L643-L847 | Indexed chunks and update/delete requests | Vespa feed/update/delete operations | Uses document/chunk counts and deletes old chunks in source path. | Live stale chunk behavior not validated. | OBSERVATION |
