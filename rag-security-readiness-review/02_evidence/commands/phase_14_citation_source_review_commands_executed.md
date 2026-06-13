
# PHASE 14 Citation/Source Review Commands Executed

This log records the source-only inspection commands used for PHASE 14. No application tests, CI, or exploit tests were run.

## Repository / environment checks
- `pwd`
- `git rev-parse --show-toplevel`
- `git branch --show-current`
- `git rev-parse HEAD`
- `git status --short`
- `find .. -name AGENTS.md -print`

## Prior-phase evidence inspection
- `sed -n '1,220p' rag-security-readiness-review/03_reports/phase_13_prompt_injection_review_report.md`
- `sed -n '1,220p' rag-security-readiness-review/03_reports/phase_12_document_ingestion_review_report.md`
- `sed -n '1,220p' rag-security-readiness-review/03_reports/phase_11_retrieval_acl_review_report.md`
- `find rag-security-readiness-review/02_evidence/phase_13 -maxdepth 3 -type f | sort`
- `find rag-security-readiness-review/02_evidence/phase_12 -maxdepth 3 -type f | sort`
- `find rag-security-readiness-review/02_evidence/phase_11 -maxdepth 3 -type f | sort`

## Source inspection commands
- `nl -ba backend/onyx/chat/citation_processor.py | sed -n '1,700p'`
- `nl -ba backend/onyx/chat/citation_processor.py | sed -n '215,531p'`
- `nl -ba backend/onyx/chat/citation_processor.py | sed -n '324,410p'`
- `nl -ba backend/onyx/chat/citation_utils.py | sed -n '1,260p'`
- `nl -ba backend/onyx/tools/tool_implementations/utils.py | sed -n '1,180p'`
- `nl -ba backend/onyx/tools/tool_runner.py | sed -n '220,460p'`
- `nl -ba backend/onyx/context/search/models.py | sed -n '235,460p'`
- `nl -ba backend/onyx/connectors/web/connector.py | sed -n '400,620p'`
- `nl -ba backend/onyx/file_processing/extract_file_text.py | sed -n '150,365p'`
- `nl -ba backend/onyx/db/models.py | sed -n '940,1075p'`
- `nl -ba backend/onyx/db/models.py | sed -n '3409,3458p'`
- `nl -ba backend/onyx/access/models.py | sed -n '1,240p'`
- `nl -ba backend/onyx/db/document.py | sed -n '120,240p'`
- `nl -ba backend/onyx/db/document.py | sed -n '650,740p'`
- `nl -ba backend/onyx/server/query_and_chat/session_loading.py | sed -n '476,630p'`
- `nl -ba backend/onyx/server/query_and_chat/session_loading.py | sed -n '840,900p'`
- `nl -ba backend/onyx/chat/llm_loop.py | sed -n '650,1085p'`
- `nl -ba web/src/components/search/results/Citation.tsx | sed -n '1,220p'`
- `nl -ba web/src/components/search/DocumentDisplay.tsx | sed -n '1,240p'`
- `nl -ba web/src/refresh-components/buttons/source-tag/SourceTag.tsx | sed -n '1,560p'`
- `nl -ba web/src/refresh-components/buttons/source-tag/SourceTagDetailsCard.tsx | sed -n '1,260p'`
- `nl -ba web/src/app/app/message/messageComponents/timeline/renderers/search/SearchChipList.tsx | sed -n '1,220p'`
- `nl -ba web/src/lib/sources.ts | sed -n '460,520p'`
- `rg -n "citation|cite|source|metadata|attribution|reference|hallucinated|spoof|stale|deleted|inaccessible|unauthorized|render|frontend" backend/tests web/tests tests 2>/dev/null || true`
- `find backend/tests web/tests tests -type f 2>/dev/null | sort | rg -i "citation|cite|source|metadata|attribution|reference|hallucinated|spoof|stale|deleted|inaccessible|unauthorized|render|frontend|search|chat"`

## No tests run
- No application tests were executed.
- No CI was executed.
- No exploit tests were executed.
