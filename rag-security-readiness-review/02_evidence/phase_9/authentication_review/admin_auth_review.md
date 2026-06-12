# Admin-only access review

## Confirmed backend enforcement
- The backend uses `require_permission(Permission.FULL_ADMIN_PANEL_ACCESS)` for admin-only actions such as changing user roles, listing accepted users, and managing API keys. 【F:backend/onyx/server/manage/users.py†L137-L203】【F:backend/onyx/server/api_key/api.py†L20-L62】
- The backend also has a broader `current_curator_or_admin_user()` helper that permits `GLOBAL_CURATOR`, `CURATOR`, and `ADMIN`. 【F:backend/onyx/auth/users.py†L1974-L1983】
- OAuth config management uses that broader curator/admin helper rather than full admin-panel access. 【F:backend/onyx/server/features/oauth_config/api.py†L36-L149】

## Confirmed frontend enforcement
- The admin route tree is wrapped in `requireAdminAuth()`, and the helper redirects any authenticated non-admin role to `/app`. 【F:web/src/layouts/admin/Layout.tsx†L11-L25】【F:web/src/lib/auth/requireAuth.ts†L74-L119】
- `requireAdminAuth()` considers `ADMIN`, `CURATOR`, and `GLOBAL_CURATOR` as allowed admin roles. 【F:web/src/lib/auth/requireAuth.ts†L74-L119】
- The cloud impersonation page is a separate gate: it redirects unauthenticated users to `/auth/login` and non-cloud-superusers to `/app`. 【F:web/src/app/auth/impersonate/page.tsx†L20-L29】

## Additional role-based gating
- The connector detail page allows inline file management for `GLOBAL_CURATOR` when the connector is public, even if the normal editable flag is false. 【F:web/src/app/admin/connector/[ccPairId]/page.tsx†L186-L190】

## Confirmed tests
- The permission tests assert that `admin` expands to all permissions and that scoped tokens are capped by the token’s own permissions. 【F:backend/tests/unit/onyx/auth/test_permissions.py†L96-L131】【F:backend/tests/unit/onyx/auth/test_permissions.py†L175-L308】
- The admin E2E suite authenticates with admin storage state before visiting `/admin/*` pages. 【F:web/tests/e2e/admin/admin_auth.setup.ts†L1-L9】【F:web/tests/e2e/admin/admin_pages.spec.ts†L1-L90】

## Client-ready note
- Admin access is not one single gate in this repository. Some routes require full admin-panel access, some allow curator/admin roles, and the frontend admin layout treats curator/global-curator/admin as the allowed admin set. 【F:backend/onyx/server/manage/users.py†L137-L203】【F:backend/onyx/server/features/oauth_config/api.py†L36-L149】【F:web/src/lib/auth/requireAuth.ts†L74-L119】
