> This is the client-facing mirror of the PHASE 11 retrieval ACL review file. The canonical evidence copy remains under rag-security-readiness-review/02_evidence/phase_11/.

# Deleted / Stale Document Handling

## Deleted document filtering
`backend/onyx/db/document_access.py` explicitly excludes `ConnectorCredentialPairStatus.DELETING` before applying public, document-public, email, or group-based access predicates. That is source-level deletion-aware filtering, but it does not validate live index behavior.

## Restricted/private document handling
`backend/onyx/access/models.py` and `backend/ee/onyx/access/access.py` encode private-vs-public behavior by building `DocumentAccess` objects with public and group/email grants. This shows how private access is represented in source, not runtime enforcement.

## Stale index entries
`backend/ee/onyx/external_permissions/post_query_censoring.py` can censor post-query results by source, and `backend/onyx/document_index/opensearch/search.py` / `backend/onyx/document_index/vespa/chunk_retrieval.py` apply hidden/ACL filters during retrieval construction. No live evidence shows whether stale index entries are fully removed in time.

## Stale connector permissions
`backend/onyx/db/connector.py` records `last_time_perm_sync` and `last_time_external_group_sync`, while `backend/ee/onyx/background/celery/tasks/external_group_syncing/tasks.py` skips DELETING pairs and uses those timestamps to decide whether another sync is due. This is a freshness model, not proof of perfect freshness.

## Reindex/delete sync behavior
`backend/ee/onyx/db/external_perm.py` marks stale external-group mappings and removes them. `backend/ee/onyx/background/celery/tasks/external_group_syncing/tasks.py` performs stale cleanup and resync scheduling. Runtime deletion and reindex timing were not validated here.

## Permission sync delay
The source explicitly supports delayed synchronization via timestamps and background tasks. The size of any exposure window remains UNVERIFIED because no live or test evidence was collected.

## Missing runtime evidence
- No live deletion timing trace.
- No live permission-sync trace.
- No live search-result retention trace after deletion.
- No search ACL regression test execution.

## Client-ready summary
The source shows deletion- and staleness-aware hooks in the retrieval and permission-sync stack, but this phase did not validate whether stale permissions or deleted documents are removed from search results quickly enough in practice.
