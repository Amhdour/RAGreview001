> This is the client-facing mirror of the PHASE 10A authorization review file. The canonical evidence copy remains under rag-security-readiness-review/02_evidence/phase_10/authorization_review/.

# Authorization Findings

## Confirmed authorization findings

### 1. Source-level permission framework exists
- Status: CONFIRMED
- Evidence: `backend/onyx/db/enums.py`, `backend/onyx/auth/permissions.py`, `backend/onyx/db/models.py`. `【F:backend/onyx/db/enums.py†L490-L554】`; `【F:backend/onyx/auth/permissions.py†L24-L127】`; `【F:backend/onyx/db/models.py†L312-L375】`
- What is confirmed: Permissions, implied permissions, admin override, and effective-permission storage are implemented in source.
- What is not confirmed: Runtime correctness and exhaustive route coverage.
- Impact: This is the core authorization vocabulary used by the rest of the system.
- Client-ready wording: The codebase contains a concrete permission model with admin override and implied permission logic.

### 2. Backend admin enforcement exists on protected routes
- Status: CONFIRMED
- Evidence: `backend/onyx/server/manage/users.py`, `backend/onyx/server/features/oauth_config/api.py`. `【F:backend/onyx/server/manage/users.py†L137-L176】`; `【F:backend/onyx/server/features/oauth_config/api.py†L63-L144】`
- What is confirmed: Admin-only routes and curator/admin-mixed routes are guarded with backend dependencies.
- What is not confirmed: Runtime allow/deny behavior for every protected route.
- Impact: Sensitive management actions are not left unguarded at the source level.
- Client-ready wording: Backend route dependencies enforce admin or curator/admin access on key management endpoints.

### 3. Curator and global curator logic is present in backend helpers
- Status: CONFIRMED
- Evidence: `backend/onyx/auth/users.py`, `backend/ee/onyx/db/user_group.py`, `backend/onyx/db/document_set.py`. `【F:backend/onyx/auth/users.py†L1974-L1983】`; `【F:backend/ee/onyx/db/user_group.py†L817-L825】`; `【F:backend/onyx/db/document_set.py†L40-L87】`
- What is confirmed: Curator and global curator roles are recognized separately from full admin.
- What is not confirmed: Exhaustive runtime coverage of all curator-sensitive endpoints.
- Impact: The code distinguishes curator privileges from full administrative privileges.
- Client-ready wording: The repository includes curator-aware authorization logic rather than a single all-or-nothing admin check.

### 4. Document and group access are represented in source
- Status: CONFIRMED
- Evidence: `backend/onyx/db/models.py`, `backend/onyx/db/document_access.py`, `backend/ee/onyx/access/access.py`. `【F:backend/onyx/db/models.py†L963-L1036】`; `【F:backend/onyx/db/document_access.py†L31-L88】`; `【F:backend/ee/onyx/access/access.py†L43-L117】`
- What is confirmed: Document-level public flags, owner fields, external-user emails, external-user groups, and group-based access are modeled and consumed.
- What is not confirmed: Runtime document visibility for every source connector.
- Impact: Retrieval exposure depends on these fields and filters.
- Client-ready wording: Document access is controlled through a combination of ownership, public flags, external groups, and group membership.

### 5. Permission-sync plumbing exists for connector and external-group state
- Status: CONFIRMED
- Evidence: `backend/ee/onyx/db/external_perm.py`, `backend/ee/onyx/background/celery/tasks/doc_permission_syncing/tasks.py`, `backend/ee/onyx/connectors/perm_sync_valid.py`, `backend/onyx/db/connector.py`. `【F:backend/ee/onyx/db/external_perm.py†L67-L216】`; `【F:backend/ee/onyx/background/celery/tasks/doc_permission_syncing/tasks.py†L1026-L1100】`; `【F:backend/ee/onyx/connectors/perm_sync_valid.py†L7-L60】`; `【F:backend/onyx/db/connector.py†L330-L356】`
- What is confirmed: The source includes sync validation, stale cleanup, and sync-completion markers.
- What is not confirmed: Real-world sync correctness and timeliness.
- Impact: Permission drift risk is explicitly handled in code, but not runtime-validated here.
- Client-ready wording: The repository contains permission-sync machinery, including validation and stale-state cleanup.

## Unverified authorization risks

### 1. Runtime authorization enforcement remains unverified
- Status: UNVERIFIED
- Why unverified: No tests, live requests, or CI were run.
- Missing evidence: Execution record for admin/basics/curator routes.
- Later validation method: Run targeted integration and E2E authorization checks.
- Client-ready wording: Source-level authorization exists, but runtime enforcement still needs validation.

### 2. Search/retrieval ACL effectiveness remains unverified
- Status: UNVERIFIED
- Why unverified: The access filters are present in source, but this phase did not execute retrieval tests.
- Missing evidence: Search-time ACL output or integration test results.
- Later validation method: Run the multitenant search-permission integration test and record output.
- Client-ready wording: Retrieval ACL logic is present in source, but runtime behavior is not yet proven here.

### 3. Connector permission sync correctness remains unverified
- Status: UNVERIFIED
- Why unverified: Sync code exists, but the jobs were not executed.
- Missing evidence: Sync-job logs, sync result records, or connector validation output.
- Later validation method: Run permission-sync jobs and capture logs plus resulting DB state.
- Client-ready wording: Connector permission-sync logic is implemented, but its runtime accuracy is not yet validated.

### 4. Frontend gating is not proof of backend enforcement
- Status: UNVERIFIED
- Why unverified: The frontend contains role-based redirects and UI gates, but no backend request validation was run here.
- Missing evidence: Live backend deny/allow evidence for the same route set.
- Later validation method: Pair browser navigation with backend response checks.
- Client-ready wording: The UI hides or redirects some admin views, but that alone does not prove backend authorization.

### 5. Tenant-boundary behavior remains unverified
- Status: UNVERIFIED
- Why unverified: Tenant-aware helpers exist in source, but no tenant-isolation runtime evidence was collected.
- Missing evidence: Multi-tenant request results and tenant-scoped ACL behavior.
- Later validation method: Execute tenant-separated integration checks.
- Client-ready wording: Tenant-aware authorization code exists, but cross-tenant isolation is not runtime-proven here.

## Contradicted claims
- No contradictory evidence was identified in this source-only review.
