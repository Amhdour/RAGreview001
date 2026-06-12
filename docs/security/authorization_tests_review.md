> This is the client-facing mirror of the PHASE 10A authorization review file. The canonical evidence copy remains under rag-security-readiness-review/02_evidence/phase_10/authorization_review/.

# Authorization Tests Review

| Area | Test file | Test type | What it appears to cover | Was it executed? | Result evidence | Limitation |
| ---- | --------- | --------- | ------------------------ | ---------------- | --------------- | ---------- |
| Permission helpers | `backend/tests/unit/onyx/auth/test_permissions.py` | Unit | Permission implication logic and dependency behavior. | NO | None collected. | File exists, but no execution record was gathered. |
| Admin access | `backend/tests/integration/tests/permissions/test_admin_access.py` | Integration | Admin-only deny/allow behavior for protected routes. | NO | None collected. | No runtime proof of route enforcement. |
| Basic access | `backend/tests/integration/tests/permissions/test_basic_access.py` | Integration | Basic-access endpoints versus denied users. | NO | None collected. | No runtime proof of basic-user access. |
| User role permissions | `backend/tests/integration/tests/permissions/test_user_role_permissions.py` | Integration | Role changes for admin/basic/curator/global curator users. | NO | None collected. | No execution evidence. |
| Document-set permissions | `backend/tests/integration/tests/permissions/test_doc_set_permissions.py` | Integration | Document-set access and visibility rules. | NO | None collected. | No runtime proof of document-set authorization. |
| Connector permissions | `backend/tests/integration/tests/permissions/test_connector_permissions.py` | Integration | Connector access and connector-level authz. | NO | None collected. | No execution evidence. |
| Credential permissions | `backend/tests/integration/tests/permissions/test_credential_permissions.py` | Integration | Credential ownership / access behavior. | NO | None collected. | No runtime proof collected. |
| Permission propagation | `backend/tests/integration/tests/permissions/test_auth_permission_propagation.py` | Integration | Propagation of permissions to users. | NO | None collected. | No execution evidence. |
| Curator flow | `backend/tests/integration/tests/permissions/test_whole_curator_flow.py` | Integration | End-to-end curator authorization flow. | NO | None collected. | Not run. |
| Search ACL | `backend/tests/integration/multitenant_tests/syncing/test_search_permissions.py` | Integration | Search-time permission synchronization and ACL behavior. | NO | None collected. | No runtime search result proof. |
| Doc permission sync attempt | `backend/tests/external_dependency_unit/permission_sync/test_doc_permission_sync_attempt.py` | External dependency unit | Document permission-sync attempt behavior. | NO | None collected. | Not executed. |
| External group sync attempt | `backend/tests/external_dependency_unit/permission_sync/test_external_group_permission_sync_attempt.py` | External dependency unit | External-group permission sync attempt behavior. | NO | None collected. | Not executed. |
| Permission-sync route attempts | `backend/tests/external_dependency_unit/permission_sync/test_cc_pair_sync_attempts_routes.py` | External dependency unit | Sync attempt route behavior. | NO | None collected. | Not executed. |
| Admin pages UI | `web/tests/e2e/admin/admin_pages.spec.ts` | E2E | Admin navigation and visible admin-page coverage. | NO | None collected. | No browser execution. |
| Groups admin UI | `web/tests/e2e/admin/groups/groups.spec.ts` | E2E | Group management UI and group CRUD flows. | NO | None collected. | No browser execution. |
| Users admin UI | `web/tests/e2e/admin/users/users.spec.ts` | E2E | Users page, role edits, filters, and group management UI. | NO | None collected. | No browser execution. |
| Connector permission-sync UI | `web/tests/e2e/admin/connector/permission-sync-tabs.spec.ts` | E2E | Connector sync tabs and permission-sync UI. | NO | None collected. | No browser execution. |
