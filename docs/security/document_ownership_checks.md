> This is the client-facing mirror of the PHASE 10A authorization review file. The canonical evidence copy remains under rag-security-readiness-review/02_evidence/phase_10/authorization_review/.

# Document Ownership Checks

## Document ownership evidence
- The document model stores `primary_owners` and `secondary_owners`. `【F:backend/onyx/db/models.py†L1010-L1018】`
- The document model also tracks `is_public`, external-user emails, and external-user group IDs. `【F:backend/onyx/db/models.py†L1019-L1036】`

## Document access filtering evidence
- `backend/onyx/db/document_access.py` filters by public connector, document public flag, user email, and external-group overlap. `【F:backend/onyx/db/document_access.py†L31-L88】`
- `backend/onyx/db/document.py` calls that filter when fetching accessible documents. `【F:backend/onyx/db/document.py†L383-L445】`
- `backend/onyx/access/access.py` treats anonymous users as public-only. `【F:backend/onyx/access/access.py†L114-L128】`

## Document set evidence
- `DocumentSet` carries `user_id`, `is_public`, `users`, and `groups` relationships. `【F:backend/onyx/db/models.py†L3408-L3465】`
- The EE document-set helper loads document sets via public, shared-user, and group membership paths. `【F:backend/ee/onyx/db/document_set.py†L54-L123】`

## Group/document relationship evidence
- `DocumentSet__UserGroup` exists as a join table, and EE code populates it when a set is made private. `【F:backend/onyx/db/models.py†L4431-L4440】`; `【F:backend/ee/onyx/db/document_set.py†L14-L40】`
- `backend/ee/onyx/access/access.py` adds user-group names to document access. `【F:backend/ee/onyx/access/access.py†L43-L117】`

## Deleted/restricted/private document behavior
- Connector deletion status is excluded from document access filtering. `【F:backend/onyx/db/document_access.py†L66-L88】`
- Public/private behavior is represented in the model and access helpers, but runtime correctness is not proven here. `【F:backend/onyx/db/models.py†L1030-L1036】`; `【F:backend/ee/onyx/access/access.py†L99-L117】`

## Retrieval/document access relationship
- Search requests are built with `bypass_acl=False`, which indicates ACL-aware retrieval flow. `【F:backend/onyx/server/features/search/api.py†L156-L170】`
- The access helper returns document ACL data that is consumed by downstream search/retrieval code. `【F:backend/onyx/access/access.py†L74-L128】`

## Gaps and unverified areas
- No runtime retrieval test was executed.
- No live document ACL sample was inspected.
- No end-to-end confirmation exists that every retrieval path honors these filters.
