# PHASE 11 Retrieval ACL Review Commands Executed

- `pwd`
- `git rev-parse --show-toplevel`
- `git branch --show-current`
- `git rev-parse HEAD`
- `git status --short`
- `test -f rag-security-readiness-review/03_reports/phase_10_control_gap_analysis_report.md && echo EXISTS || echo NOT_AVAILABLE`
- `test -f rag-security-readiness-review/02_evidence/phase_8/retrieval_acl_risk_to_code.md && echo EXISTS || echo NOT_AVAILABLE`
- `test -f rag-security-readiness-review/02_evidence/phase_9/retrieval_acl_test_evidence.md && echo EXISTS || echo NOT_AVAILABLE`
- `find rag-security-readiness-review/02_evidence/phase_10 -maxdepth 3 -type f | sort`
- `find rag-security-readiness-review/02_evidence/phase_9 -maxdepth 3 -type f | sort`
- `find rag-security-readiness-review/02_evidence/phase_8 -maxdepth 3 -type f | sort`
- `find rag-security-readiness-review/02_evidence/phase_5 -maxdepth 2 -type f | sort`
- `rg --files backend web docs rag-security-readiness-review/02_evidence | rg -i "retrieval|retrieve|search|query|document|document_set|acl|access|permission|filter|tenant|workspace|group|connector|credential|visibility|private|public|deleted|restricted|stale|source|citation|chunk|vespa|opensearch|elastic|vector|keyword|hybrid|rerank|permission_sync|metadata" | sort`
- `rg -n -i "retrieval|retrieve|search|query|document|document_id|document_set|acl|access|permission|permissions|filter|filters|tenant|workspace|group|user_group|connector|credential|cc_pair|visibility|private|public|deleted|restricted|stale|source|citation|chunk|chunk_id|vespa|opensearch|elastic|vector|keyword|hybrid|rerank|reranker|validated_document_ids|permission_sync|sync|source_metadata|metadata" backend web docs rag-security-readiness-review/02_evidence 2>/dev/null || true`
- `find backend/tests web/tests tests -type f 2>/dev/null | sort`
- `rg -n -i "retrieval|search|document|acl|access|permission|tenant|group|connector|deleted|restricted|stale|rerank|permission_sync|metadata" backend/tests web/tests tests 2>/dev/null || true`
- Additional targeted `nl -ba` and `rg -n` inspections of the source files cited in this package.
