# PHASE 11 Retrieval ACL Security Review

## Scope
This phase reviews retrieval ACL security as a source-only evidence exercise. It traces how document-access information flows through retrieval entry points, preprocessing, ACL filter construction, vector and keyword search backends, reranking assumptions, deleted/stale document handling, cross-user/group/connector risk paths, and cited/source rendering.

## Evidence basis
Evidence is limited to the current checkout and previously produced phase artifacts. No runtime traces, test execution output, CI output, production output, live database output, or live search-index output were collected in this phase.

Primary source evidence reviewed in this pass includes:
- `backend/onyx/server/features/search/api.py`
- `backend/ee/onyx/server/query_and_chat/search_backend.py`
- `backend/onyx/server/query_and_chat/chat_backend.py`
- `backend/onyx/server/query_and_chat/query_backend.py`
- `backend/onyx/context/search/pipeline.py`
- `backend/onyx/context/search/retrieval/search_runner.py`
- `backend/onyx/tools/tool_implementations/search/search_tool.py`
- `backend/onyx/document_index/vespa/shared_utils/vespa_request_builders.py`
- `backend/onyx/document_index/vespa/chunk_retrieval.py`
- `backend/onyx/document_index/opensearch/search.py`
- `backend/onyx/db/document_access.py`
- `backend/onyx/access/access.py`
- `backend/ee/onyx/access/access.py`
- `backend/ee/onyx/external_permissions/post_query_censoring.py`
- `backend/ee/onyx/background/celery/tasks/external_group_syncing/tasks.py`
- `backend/ee/onyx/db/external_perm.py`
- `backend/onyx/chat/citation_utils.py`
- `web/src/components/search/results/Citation.tsx`

## Retrieval ACL review method
1. Start from PHASE 10 GAP-10-005 and the prior phase evidence package.
2. Trace retrieval entry points from frontend to backend.
3. Trace search preprocessing, request normalization, and context injection.
4. Trace ACL filter construction into Vespa and OpenSearch query builders.
5. Trace the inputs used to create retrieval filters.
6. Separate vector-search, keyword-search, and hybrid-search paths.
7. Inspect reranking and post-retrieval selection ordering.
8. Inspect bypass-prone and stale-state-sensitive paths.
9. Review discovered tests and evidence files without executing them.
10. Classify each claim as confirmed, observation, or unverified risk.

## Retrieval ACL areas reviewed
- Search API and chat/search API entry points.
- Search preprocessing and request normalization.
- ACL filter construction and propagation.
- ACL input sources.
- Vector, keyword, and hybrid retrieval backends.
- Reranking and LLM selection ordering.
- Direct document-id and admin-oriented paths.
- Deleted, restricted, private, and stale state handling.
- Cross-user, cross-group, cross-tenant, and cross-connector exposure risks.
- Search ACL test evidence discovered in the repository.

## Confirmed findings summary
- Source-level retrieval ACL filters are built from user, group, document-set, source, tag, tenant, time, persona, project, and attached-document inputs before search requests are dispatched.
- Document access filtering explicitly excludes connector pairs in `DELETING` status and only allows access through public, document-public, email, or group overlap predicates.
- Both Vespa and OpenSearch query builders carry ACL-related filters into retrieval requests rather than relying only on post-processing.
- The search tool performs ranking fusion and later LLM selection after retrieval, so source-level filter propagation exists before later ranking/selection stages.

## Observations summary
- Multiple frontend paths call backend search endpoints directly, including search classification, search submission, and search history retrieval.
- Search history stores query history per user, but it does not itself demonstrate retrieval authorization.
- Citation rendering uses source type and semantic title for display and opens the document from the search result object; this is not itself an ACL check.
- Admin search deliberately exposes hidden documents to privileged users, which is consistent with the code but should not be generalized to ordinary search.

## Unverified risks summary
- Runtime ACL enforcement was not validated, so source-level filter construction does not prove effective enforcement.
- Direct document-id retrieval paths are guarded by the assumption that prior validation already happened, but that assumption was not runtime-tested here.
- Permission-sync lag, stale external-group mappings, or stale index entries could leave a temporary exposure window, but no runtime proof was collected.
- Cross-user, cross-group, cross-tenant, and cross-connector leakage risks remain unverified without runtime or test execution.

## Missing evidence
- No test execution evidence was collected in this phase.
- No CI evidence was collected in this phase.
- No runtime search-trace or ACL-enforcement trace was collected.
- No production/live-search evidence was collected.
- No live database, vector index, or search index inspection was collected.
- No customer-data or real-secret evidence was used.

## Limitations
- Source-only limitation.
- Current-checkout limitation.
- Original source unavailable.
- Working copy unavailable.
- Tests discovered but not executed.
- CI not executed.
- Runtime retrieval behavior not validated.
- Runtime ACL enforcement not validated.
- Production behavior not validated.
- Live database, vector index, search index, and connector-state evidence unavailable.

## Non-claims
- This phase does not claim retrieval ACL enforcement is effective.
- This phase does not claim tests passed.
- This phase does not claim production readiness.
- This phase does not claim exploitability.
- This phase does not claim all runtime paths are covered.

## Client-ready summary
The reviewed source shows retrieval ACL construction and propagation through the search stack, but the phase remains source-only. The package is useful for understanding how ACL inputs are intended to flow through retrieval, yet it does not validate runtime enforcement or prove that unauthorized retrieval is blocked in practice.
