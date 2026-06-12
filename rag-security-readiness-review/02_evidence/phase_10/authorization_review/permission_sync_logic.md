# Permission Sync Logic

## Permission sync files
- `backend/ee/onyx/db/external_perm.py`
- `backend/ee/onyx/db/user_group.py`
- `backend/ee/onyx/background/celery/tasks/doc_permission_syncing/tasks.py`
- `backend/ee/onyx/background/celery/tasks/external_group_syncing/tasks.py`
- `backend/ee/onyx/background/celery/tasks/external_group_syncing/group_sync_utils.py`
- `backend/ee/onyx/connectors/perm_sync_valid.py`
- `backend/onyx/db/connector.py`

## Permission sync flow
- External-group sync reads source permissions, upserts user-group mappings, and removes stale rows. `【F:backend/ee/onyx/db/external_perm.py†L67-L216】`
- Document-permission sync updates the permission-sync fence and sync completion state. `【F:backend/ee/onyx/background/celery/tasks/doc_permission_syncing/tasks.py†L1026-L1100】`
- Connector timestamps are updated after sync completion. `【F:backend/onyx/db/connector.py†L330-L356】`

## Sync trigger or job evidence
- External-group sync task code calls `mark_old_external_groups_as_stale()`, `upsert_external_groups()`, and `remove_stale_external_groups()`. `【F:backend/ee/onyx/background/celery/tasks/external_group_syncing/tasks.py†L533-L641】`
- Direct scheduling/trigger coverage for every permission-sync path is UNVERIFIED in this phase because no runtime worker or beat schedule validation was performed.

## Failure handling evidence
- Connector sync validation functions are explicit probes for misconfigured permission surfaces. `【F:backend/ee/onyx/connectors/perm_sync_valid.py†L7-L60】`
- External-group sync uses stale cleanup to reduce drift if a prior cycle failed. `【F:backend/ee/onyx/db/external_perm.py†L67-L85】`

## Stale permission risks
- The code acknowledges stale external-group state and includes cleanup paths for it. `【F:backend/ee/onyx/db/external_perm.py†L67-L85】`; `【F:backend/ee/onyx/background/celery/tasks/external_group_syncing/tasks.py†L533-L641】`
- Document permission upserts preserve existing permission fields when later indexing runs do not include them. `【F:backend/onyx/db/document.py†L718-L743】`

## Missing runtime evidence
- No sync job was executed in this phase.
- No live connector was validated.
- No stale-state recovery was runtime-tested.

## Client-ready summary
The repository includes explicit permission-sync plumbing for external groups, document permissions, and connector sync state. That is strong source evidence, but runtime correctness still needs later validation.
