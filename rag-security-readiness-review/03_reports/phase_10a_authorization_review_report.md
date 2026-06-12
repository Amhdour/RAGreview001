# PHASE 10A Authorization Review Report

## Executive summary
PHASE 10A completed a focused authorization evidence review. The repository contains a clear source-level permission model, backend route gates, curator-aware helpers, document/group access filters, and permission-sync plumbing. This phase did not validate runtime effectiveness.

## Evidence basis
- Current checkout only.
- Previous PHASE 8 and PHASE 9 evidence files were read first.
- No application tests, CI, or exploit tests were run.

## Permission model summary
The code defines explicit permission tokens, implied-permission expansion, a user-level effective-permissions column, and group-level permission grants. `【F:backend/onyx/db/enums.py†L490-L554】`; `【F:backend/onyx/auth/permissions.py†L24-L127】`; `【F:backend/onyx/db/models.py†L312-L375】`; `【F:backend/onyx/db/models.py†L4308-L4352】`.

## Role-check summary
The source distinguishes basic, admin, curator, global curator, limited, Slack, and external-permission users. Backend helpers and frontend allowlists both recognize curator/global-curator behavior. `【F:backend/onyx/auth/schemas.py†L11-L31】`; `【F:backend/onyx/auth/users.py†L1974-L1983】`; `【F:web/src/lib/auth/requireAuth.ts†L74-L119】`.

## Admin/curator summary
Admin-only routes use backend dependencies, while some EE routes allow curator/admin access. Frontend admin layout gating mirrors that role split, but frontend gating alone is not proof of backend enforcement. `【F:backend/onyx/server/manage/users.py†L137-L176】`; `【F:backend/onyx/server/features/oauth_config/api.py†L63-L144】`; `【F:web/src/layouts/admin/Layout.tsx†L11-L18】`.

## Document ownership summary
Documents carry owner and external-access fields, and the access filter includes connector public state, document public state, email matches, and external group overlap. `【F:backend/onyx/db/models.py†L963-L1036】`; `【F:backend/onyx/db/document_access.py†L31-L88】`.

## Group/workspace permission summary
User-group relationships, curator flags, group-to-document-set links, and group grants are all present. Tenant-aware anonymous access is also represented in source. `【F:backend/onyx/db/models.py†L4293-L4515】`; `【F:backend/ee/onyx/db/user_group.py†L293-L315】`; `【F:backend/onyx/auth/users.py†L230-L239】`.

## Connector permission summary
Connector credential pairs track access type and permission-sync state, and EE validation logic probes source permissions before sync. `【F:backend/onyx/db/models.py†L747-L856】`; `【F:backend/onyx/db/connector.py†L330-L356】`; `【F:backend/ee/onyx/connectors/perm_sync_valid.py†L7-L60】`.

## Backend/frontend enforcement summary
Backend dependency checks are the authoritative enforcement layer. Frontend route gating and UI restrictions exist, but they are only defense-in-depth. `【F:backend/onyx/auth/permissions.py†L101-L127】`; `【F:web/src/lib/auth/requireAuth.ts†L99-L119】`; `【F:web/src/components/IsPublicGroupSelector.tsx†L33-L124】`.

## Permission sync summary
Permission sync is implemented through external-permission upserts, stale cleanup, connector sync timestamps, and task code. Direct scheduling coverage for every sync path is unverified because runtime workers and beat scheduling were not validated. `【F:backend/ee/onyx/db/external_perm.py†L67-L216】`; `【F:backend/ee/onyx/background/celery/tasks/external_group_syncing/tasks.py†L533-L641】`; `【F:backend/ee/onyx/background/celery/tasks/doc_permission_syncing/tasks.py†L1026-L1100】`.

## Authorization test summary
Relevant unit, integration, external-dependency, and E2E test files were discovered, including `backend/tests/unit/onyx/auth/test_permissions.py`, `backend/tests/integration/tests/permissions/test_admin_access.py`, and `backend/tests/integration/multitenant_tests/syncing/test_search_permissions.py`. None were executed in this phase.

## Confirmed findings
- Source-level permission framework exists.
- Backend admin and curator enforcement points exist.
- Document/group access filtering exists in source.
- Connector permission-sync plumbing exists in source.
- Frontend admin gating exists, but it is not the authoritative control.

## Unverified risks
- Runtime authorization enforcement.
- Retrieval ACL effectiveness.
- Connector permission-sync correctness.
- Tenant-boundary behavior.
- Frontend/backend alignment at runtime.

## Missing evidence
- No test execution output.
- No live deny/allow proof.
- No runtime ACL proof.
- No sync-job execution proof.

## Limitations
- Source-only limitation.
- Current-checkout limitation.
- Original source unavailable.
- Working copy unavailable.
- Tests discovered but not executed.
- CI not executed.
- No runtime validation.
- No production validation.
- No exploit validation.
- Frontend gating is not proof of backend enforcement.

## Non-claims
- No claim of production readiness.
- No claim that discovered test files passed.
- No claim that all authorization paths were exhaustively verified.

## Status
COMPLETE WITH LIMITATIONS

## Exact next step
PHASE 10 — Create control gap analysis
