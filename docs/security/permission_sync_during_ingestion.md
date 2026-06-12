> This is the client-facing mirror of the PHASE 12 document ingestion review file. The canonical evidence copy remains under rag-security-readiness-review/02_evidence/phase_12/.

# PHASE 12 — Permission Sync During Ingestion

## Permission sync trigger

Checkpointed connector interfaces include `include_permissions` in source-level reindex contracts (`backend/onyx/connectors/interfaces.py` L240-L329). Selected connectors expose permission-sync slim-document retrieval paths, including Confluence (`backend/onyx/connectors/confluence/connector.py` L1028-L1065) and Google Drive (`backend/onyx/connectors/google_drive/connector.py` L1838-L2038).

## Permission sync state

Permission-sync attempt database helpers create and update permission-sync attempt records in `backend/onyx/db/permission_sync_attempt.py` L36-L56 and L120-L245. External group sync attempt helpers are in the same file L257-L530.

## Group/user permission ingestion

Document access metadata is persisted in source-level document upsert logic in `backend/onyx/db/document.py` L649-L743, including external user emails, external user group IDs, and public access fields. Access info collection is also source-visible in `backend/onyx/db/document.py` L600-L646.

## Connector permission ingestion

Permission-aware connector interfaces and selected connector implementations establish source-level connector permission ingestion paths. Runtime connector-specific permission correctness was not validated.

## Permission update timing

The source-level metadata sync task builds index metadata update requests from current DB access/document-set state in `backend/onyx/background/celery/tasks/vespa/tasks.py` L460-L579. Runtime ordering between document content ingestion, permission-sync completion, and retrieval availability was not validated.

## Failure handling

Permission-sync attempt status helpers exist in `backend/onyx/db/permission_sync_attempt.py` L120-L245 and L257-L530. PHASE 12 did not execute failure scenarios or validate recovery behavior.

## Stale permission behavior

Stale permission behavior remains UNVERIFIED. Source-level code includes permission/access metadata persistence and sync attempts, but PHASE 12 did not validate live connector permission changes, live DB access state, live index metadata updates, or retrieval ACL outcomes.

## Relationship to retrieval ACL filters

PHASE 11 reviewed retrieval ACL source paths and stale/deleted document implications with limitations. PHASE 12 treats permission sync as upstream ingestion/index metadata input and does not claim runtime retrieval ACL enforcement.

## Missing runtime evidence

Missing evidence includes live connector permissions, live external group/user mappings, permission-sync task execution logs, failed-sync traces, live DB access rows, live index metadata after permission changes, and retrieval behavior under changed permissions.

## Client-ready summary

The current checkout contains source-level permission-sync contracts, attempt state helpers, access metadata persistence, and index metadata update paths. PHASE 12 does not prove that runtime permission sync is complete, timely, or effective for retrieval authorization.
