# Retrieval ACL Risk to Code

## Category purpose
Map document-level ACL, indexing, citation, and post-query censoring paths that may control whether restricted content can be retrieved or surfaced.

## Related PHASE 7 risks
- ACL-01
- ACL-02
- ACL-03
- ACL-04
- ACL-05
- RAG-01
- RAG-03
- RAG-04
- RAG-05

## Related PHASE 6 threats
- TH-01
- TH-02
- TH-03
- TH-05
- TH-06
- TH-08
- TH-09

## Related PHASE 5 architecture evidence
- rag-security-readiness-review/02_evidence/phase_5/rag_pipeline_map.md
- rag-security-readiness-review/02_evidence/phase_5/authorization_flow_map.md
- rag-security-readiness-review/02_evidence/phase_5/data_model_map.md
- rag-security-readiness-review/02_evidence/phase_5/api_routes_map.md

## Related PHASE 3 inventory evidence
- rag-security-readiness-review/02_evidence/phase_3/baseline_inventory.md
- rag-security-readiness-review/02_evidence/phase_3/important_files_index.md
- rag-security-readiness-review/02_evidence/phase_3/security_relevant_files.md

## Candidate Onyx file paths
- backend/onyx/document_index/vespa/chunk_retrieval.py
- backend/onyx/document_index/vespa/vespa_document_index.py
- backend/onyx/document_index/vespa/shared_utils/vespa_request_builders.py
- backend/ee/onyx/external_permissions/google_drive/permission_retrieval.py
- backend/ee/onyx/external_permissions/sharepoint/permission_utils.py
- backend/ee/onyx/external_permissions/confluence/page_access.py
- backend/ee/onyx/external_permissions/confluence/space_access.py
- backend/ee/onyx/external_permissions/post_query_censoring.py
- backend/onyx/chat/citation_utils.py
- backend/onyx/server/features/search/api.py
- web/src/components/search/results/Citation.tsx

## Existing control candidates
- ACL-MAP-01: retrieval and Vespa query-building paths appear available.
- ACL-MAP-02: connector permission retrieval and post-query censoring paths appear available.

## Missing control candidates
- No live ACL-enforcement evidence or deleted-content retention proof was collected.

## Unverified mappings
- ACL-MAP-03: citation privacy remains unverified.

## Later validation methods
- Live ACL enforcement review.
- Permission sync and censoring validation.
- Citation privacy testing.

## Non-claims
- No claim that citations only expose accessible sources.
- No claim that the index fully purges restricted content.

## Client-ready summary
The retrieval ACL surface is split across query paths, connector permission sync, and citation rendering, but effectiveness remains unvalidated.

## Mapping table

| Mapping ID | Related risk ID/category | Related PHASE 6 threat ID | Related PHASE 5 architecture evidence | Candidate Onyx file/path | Mapping label | Why this file/path matters | Missing evidence | Later validation method | Notes |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| ACL-MAP-01 | ACL-01 / RAG-01 | TH-01 / TH-03 | rag_pipeline_map.md; authorization_flow_map.md; data_model_map.md; api_routes_map.md | backend/onyx/document_index/vespa/chunk_retrieval.py; backend/onyx/document_index/vespa/vespa_document_index.py; backend/onyx/document_index/vespa/shared_utils/vespa_request_builders.py | EXISTING-CANDIDATE | These files are the clearest retrieval and index-query candidates for ACL filtering and result shaping. | No live document-ACL enforcement check or search-result authorization test was run. | ACL enforcement validation and index-retention review. | Source-level retrieval control candidate only. |
| ACL-MAP-02 | ACL-02 / ACL-03 / RAG-05 | TH-05 / TH-06 | rag_pipeline_map.md; authorization_flow_map.md; data_model_map.md; api_routes_map.md | backend/ee/onyx/external_permissions/google_drive/permission_retrieval.py; backend/ee/onyx/external_permissions/sharepoint/permission_utils.py; backend/ee/onyx/external_permissions/confluence/page_access.py; backend/ee/onyx/external_permissions/post_query_censoring.py | EXISTING-CANDIDATE | These files suggest upstream permission retrieval and post-query censoring that could keep the indexed corpus aligned with source access. | No live connector-permission sync review or deleted-content retention review was performed. | Permission-sync and post-query censoring validation. | Candidate control path spans connector ACL sync and downstream query censorship. |
| ACL-MAP-03 | ACL-05 / RAG-04 | TH-08 | rag_pipeline_map.md; authorization_flow_map.md; data_model_map.md; api_routes_map.md | backend/onyx/chat/citation_utils.py; backend/onyx/server/features/search/api.py; web/src/components/search/results/Citation.tsx | UNVERIFIED | These files suggest citation rendering and search response shaping, but they do not prove that inaccessible-source metadata is withheld. | No citation-privacy or source-visibility validation was collected. | Citation privacy review and source-visibility testing. | Unverified because the current pass is source-only. |
