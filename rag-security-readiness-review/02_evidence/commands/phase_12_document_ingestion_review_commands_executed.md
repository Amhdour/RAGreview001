# PHASE 12 — Document Ingestion Review Commands Executed

## Scope and safety notes

- No application tests were run.
- No CI jobs were run.
- No exploit tests were run.
- No application source code was intentionally modified.
- Commands were limited to repository inspection, source search, evidence-file creation, status checks, git add/commit, and PR creation.

## Commands

```bash
pwd && git rev-parse --show-toplevel && git branch --show-current && git rev-parse HEAD && git status --short && find .. -name AGENTS.md -print
```

```bash
sed -n '1,260p' AGENTS.md
```

```bash
test -f rag-security-readiness-review/03_reports/phase_11_retrieval_acl_review_report.md && echo EXISTS || echo NOT_AVAILABLE
test -f rag-security-readiness-review/03_reports/phase_10_control_gap_analysis_report.md && echo EXISTS || echo NOT_AVAILABLE
test -f rag-security-readiness-review/02_evidence/phase_8/ingestion_risk_to_code.md && echo EXISTS || echo NOT_AVAILABLE
test -f rag-security-readiness-review/02_evidence/phase_9/ingestion_test_evidence.md && echo EXISTS || echo NOT_AVAILABLE
```

```bash
find rag-security-readiness-review/02_evidence/phase_11 -maxdepth 3 -type f | sort
find rag-security-readiness-review/02_evidence/phase_10 -maxdepth 3 -type f | sort
find rag-security-readiness-review/02_evidence/phase_9 -maxdepth 3 -type f | sort
find rag-security-readiness-review/02_evidence/phase_8 -maxdepth 3 -type f | sort
find rag-security-readiness-review/02_evidence/phase_5 -maxdepth 2 -type f | sort
```

```bash
rg --files backend web docs rag-security-readiness-review/02_evidence | rg -i "upload|file|document|document_set|connector|cc_pair|sync|ingest|ingestion|index|indexing|reindex|embedding|embed|chunk|section|parser|parse|pdf|html|docx|office|mime|metadata|source|citation|permission|permission_sync|group|tenant|workspace|deleted|deletion|stale|restricted|private|visibility|size|archive|zip|sanitize|malicious|poison|retry|failure" | sort
```

```bash
rg -n -i "upload|uploaded|file|files|document|documents|document_id|document_set|connector|connectors|cc_pair|sync|ingestion|ingest|index|indexing|reindex|embedding|embed|chunk|chunking|section|parser|parse|pdf|html|docx|office|text|mime|file_type|extension|metadata|source_metadata|title|url|citation|source|permission|permissions|permission_sync|group|user_group|tenant|workspace|deleted|deletion|stale|restricted|private|visibility|size|oversized|archive|zip|sanitize|sanitization|malicious|prompt injection|poison|poisoning|retry|failure" backend web docs rag-security-readiness-review/02_evidence 2>/dev/null || true
```

```bash
find backend/tests web/tests tests -type f 2>/dev/null | sort
```

```bash
rg -n -i "upload|file|document|connector|sync|ingest|ingestion|index|embedding|chunk|parser|metadata|permission_sync|deleted|stale|oversized|malicious|poison" backend/tests web/tests tests 2>/dev/null || true
```

```bash
nl -ba <source-path> | sed -n '<line-range>p'
```

Used repeatedly for source-only line-reference inspection of upload, connector, parser, chunking, indexing, embedding, update/delete, permission-sync, frontend, and test source files cited in PHASE 12 evidence.

```bash
mkdir -p rag-security-readiness-review/02_evidence/phase_12/raw_outputs rag-security-readiness-review/02_evidence/commands rag-security-readiness-review/03_reports rag-security-readiness-review/06_templates/phase_12 docs/security
```

```bash
rg -n -i "upload|uploaded|file/upload|connector/file/upload|files/update|FileOrigin|upload_files" backend/onyx/server backend/onyx/db web/src web/tests 2>/dev/null > rag-security-readiness-review/02_evidence/phase_12/raw_outputs/upload_entry_points_search_raw.txt || true
rg -n -i "LoadConnector|CheckpointedConnector|retrieve_all_slim_docs_perm_sync|include_permissions|connector_runner|perm_sync|yield|raise|except" backend/onyx/connectors backend/onyx/federated_connectors backend/onyx/background/celery/tasks 2>/dev/null > rag-security-readiness-review/02_evidence/phase_12/raw_outputs/connector_ingestion_search_raw.txt || true
rg -n -i "extract_file_text|mimetypes|extension|pdf|docx|pptx|xlsx|html|zip|unsupported|password|oversize|too large|sanitize|load_files_from_zip" backend/onyx/file_processing backend/onyx/server/features/projects backend/onyx/server/documents 2>/dev/null > rag-security-readiness-review/02_evidence/phase_12/raw_outputs/file_parsing_search_raw.txt || true
rg -n -i "Chunker|chunk|chunk_overlap|metadata_suffix|section|clean_text|large chunk|IndexChunk|DocAwareChunk" backend/onyx/indexing 2>/dev/null > rag-security-readiness-review/02_evidence/phase_12/raw_outputs/document_chunking_search_raw.txt || true
rg -n -i "metadata|doc_metadata|source_metadata|title|link|semantic_id|owner|external_user|external_user_group|document_set|file_id|citation" backend/onyx/indexing backend/onyx/db backend/onyx/document_index backend/onyx/connectors/file 2>/dev/null > rag-security-readiness-review/02_evidence/phase_12/raw_outputs/metadata_extraction_search_raw.txt || true
rg -n -i "write_chunks|index|delete|update|chunk_count|document_id|vector|keyword|hybrid|opensearch|vespa|retry|failure" backend/onyx/indexing backend/onyx/document_index backend/onyx/background/celery/tasks/vespa 2>/dev/null > rag-security-readiness-review/02_evidence/phase_12/raw_outputs/indexing_logic_search_raw.txt || true
rg -n -i "embed|embedding|EmbeddingModel|encode|provider|model|retry|metadata" backend/onyx/indexing backend/onyx/llm backend/onyx/configs 2>/dev/null > rag-security-readiness-review/02_evidence/phase_12/raw_outputs/embedding_logic_search_raw.txt || true
rg -n -i "delete|deleted|deletion|stale|prune|pruning|cleanup|mark_document|sync|hard|soft|chunk_count|file_id" backend/onyx/db backend/onyx/background/celery/tasks backend/onyx/document_index backend/onyx/file_store 2>/dev/null > rag-security-readiness-review/02_evidence/phase_12/raw_outputs/document_update_delete_search_raw.txt || true
rg -n -i "permission_sync|DocPermissionSyncAttempt|external_user|external_group|include_permissions|access|ACL|retrieval ACL|perm_sync" backend/onyx/db backend/onyx/connectors backend/onyx/background/celery/tasks rag-security-readiness-review/02_evidence/phase_11 2>/dev/null > rag-security-readiness-review/02_evidence/phase_12/raw_outputs/permission_sync_ingestion_search_raw.txt || true
rg -n -i "unsafe|oversized|too large|malicious|prompt injection|poison|leak|stale|deleted|permission drift|sensitive|crash|zip|archive" backend/onyx rag-security-readiness-review/02_evidence 2>/dev/null > rag-security-readiness-review/02_evidence/phase_12/raw_outputs/ingestion_risks_search_raw.txt || true
find backend/tests web/tests tests -type f 2>/dev/null | sort | rg -i "upload|file|document|connector|sync|ingest|ingestion|index|embedding|chunk|parser|metadata|permission|deleted|stale|oversized|malicious|poison" > rag-security-readiness-review/02_evidence/phase_12/raw_outputs/ingestion_tests_search_raw.txt || true
```

```bash
python - <<'PY'
# Created canonical PHASE 12 evidence files, report, templates, and docs/security mirrors.
PY
```

```bash
git status --short
```

```bash
git add rag-security-readiness-review/02_evidence/phase_12 rag-security-readiness-review/02_evidence/commands/phase_12_document_ingestion_review_commands_executed.md rag-security-readiness-review/03_reports/phase_12_document_ingestion_review_report.md rag-security-readiness-review/06_templates/phase_12 docs/security
git commit -m "Add phase 12 document ingestion review"
```

```bash
for f in docs/security/document_ingestion_review.md docs/security/upload_entry_points.md docs/security/phase_12_document_ingestion_review_index.md; do echo '---' $f; head -n 2 "$f"; done
python - <<'PY'
from pathlib import Path
required=[...]
missing=[p for p in required if not Path(p).is_file()]
print('missing', missing)
print('raw count', len(list(Path('rag-security-readiness-review/02_evidence/phase_12/raw_outputs').glob('*.txt'))))
PY
```

```bash
python - <<'PY'
from pathlib import Path
# Validated required PHASE 12 files exist and raw output file count is 15.
PY
```

```bash
git diff --name-only -- docs/security rag-security-readiness-review | sort && git status --short
git status --short
```
