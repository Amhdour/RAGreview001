# Group and Workspace Permission Checks

## User group model
- `User__UserGroup` stores membership and curator status. `【F:backend/onyx/db/models.py†L4293-L4305】`
- `UserGroup` stores name, sync state, deletion state, and relationships to users, connectors, document sets, personas, and permissions. `【F:backend/onyx/db/models.py†L4453-L4515】`

## Group membership
- `fetch_user_groups_for_user()` returns the groups a user belongs to, with curator filtering available. `【F:backend/ee/onyx/db/user_group.py†L293-L315】`
- `fetch_user_groups_for_documents()` maps documents back to group membership. `【F:backend/ee/onyx/db/user_group.py†L395-L430】`

## Group grants
- `PermissionGrant` rows attach permissions to groups and are recomputed into user effective permissions. `【F:backend/onyx/db/models.py†L4308-L4352】`; `【F:backend/onyx/db/permissions.py†L43-L116】`
- `set_group_permission__no_commit()` soft-deletes or restores permission grants. `【F:backend/ee/onyx/db/user_group.py†L965-L1005】`

## Workspace or tenant context
- Anonymous access is tenant-aware. `【F:backend/onyx/auth/users.py†L230-L239】`; `【F:backend/onyx/auth/users.py†L1952-L1959】`
- Search also reads current tenant context when checking provider access. `【F:backend/onyx/server/features/search/api.py†L119-L124】`

## Group-based document filtering
- Document sets can be linked to groups directly in the model. `【F:backend/onyx/db/models.py†L3447-L3458】`
- EE document-set fetching includes group membership when resolving access. `【F:backend/ee/onyx/db/document_set.py†L76-L123】`

## Multi-user or multi-tenant boundary relevance
- `backend/ee/onyx/access/access.py` prefixes user-group names and external group IDs before building ACLs. `【F:backend/ee/onyx/access/access.py†L183-L210】`
- That prefixing reduces collisions across connector-derived groups, but runtime boundary correctness remains unverified.

## Gaps and unverified areas
- No runtime tenant-isolation test was run.
- No live group-membership mutation flow was exercised.
- No evidence was collected for every workspace boundary path.
