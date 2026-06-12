> This is the client-facing mirror of the PHASE 10A authorization review file. The canonical evidence copy remains under rag-security-readiness-review/02_evidence/phase_10/authorization_review/.

# Connector Permission Checks

## Connector credential ownership
- `ConnectorCredentialPair.creator_id` and `creator` capture who created a connector credential pair. `【F:backend/onyx/db/models.py†L850-L856】`
- `ConnectorCredentialPair.access_type` records whether the connector is PUBLIC or SYNC/private. `【F:backend/onyx/db/models.py†L778-L783】`

## Connector permission model
- Connector credential pairs carry sync timestamps and access type in the model. `【F:backend/onyx/db/models.py†L747-L856】`
- Document access filtering excludes connector pairs in `DELETING` state. `【F:backend/onyx/db/document_access.py†L66-L88】`

## Connector permission sync
- Permission sync timestamps are updated by `mark_cc_pair_as_permissions_synced()` and `mark_cc_pair_as_external_group_synced()`. `【F:backend/onyx/db/connector.py†L330-L356】`
- Connector-specific permission validation exists for Confluence, Google Drive, and SharePoint. `【F:backend/ee/onyx/connectors/perm_sync_valid.py†L7-L60】`
- External-group sync jobs upsert and remove stale groups. `【F:backend/ee/onyx/db/external_perm.py†L67-L216】`

## External source permission boundary
- Documents can store externally synced user emails and external group IDs. `【F:backend/onyx/db/models.py†L1019-L1036】`
- EE access code merges external groups with internal ACLs. `【F:backend/ee/onyx/access/access.py†L70-L117】`

## Stale permission risk
- External-group records have a `stale` flag and are cleaned up after sync cycles. `【F:backend/ee/onyx/db/external_perm.py†L67-L85】`; `【F:backend/ee/onyx/db/external_perm.py†L200-L216】`
- The sync tasks explicitly remove stale external groups before and after the current cycle. `【F:backend/ee/onyx/background/celery/tasks/external_group_syncing/tasks.py†L533-L641】`

## Gaps and unverified areas
- No runtime connector-permission sync validation was executed.
- No live connector source was inspected.
- No source-specific connector permission matrix was exhaustively tested.
