> This is the client-facing mirror of the PHASE 10A authorization review file. The canonical evidence copy remains under rag-security-readiness-review/02_evidence/phase_10/authorization_review/.

# Admin and Curator Checks

## Full admin checks
- `backend/onyx/server/manage/users.py` uses `require_permission(Permission.FULL_ADMIN_PANEL_ACCESS)` on user-management routes. `【F:backend/onyx/server/manage/users.py†L137-L176】`
- `backend/onyx/server/features/search/api.py` compares `user.role == UserRole.ADMIN` when deciding whether a user may access a provider. `【F:backend/onyx/server/features/search/api.py†L99-L106】`

## Curator checks
- `backend/onyx/auth/users.py` defines `current_curator_or_admin_user()` and includes curator in the allowlist. `【F:backend/onyx/auth/users.py†L1974-L1983】`
- `backend/ee/onyx/db/user_group.py` filters curator-sensitive updates so non-admin curators remain constrained by curator membership. `【F:backend/ee/onyx/db/user_group.py†L817-L825】`

## Global curator checks
- `current_curator_or_admin_user()` includes `UserRole.GLOBAL_CURATOR`. `【F:backend/onyx/auth/users.py†L1974-L1983】`
- Document-set filtering distinguishes curator behavior from global-curator access. `【F:backend/onyx/db/document_set.py†L40-L87】`

## Mixed admin/curator routes
- OAuth configuration endpoints are guarded by `current_curator_or_admin_user()`, so they are accessible to curator and admin roles rather than admin alone. `【F:backend/onyx/server/features/oauth_config/api.py†L63-L144】`
- User-group management uses curator-aware logic in the EE DB layer. `【F:backend/ee/onyx/db/user_group.py†L741-L835】`

## Frontend admin UI gates
- `requireAdminAuth()` allows admin, curator, and global curator roles into admin pages. `【F:web/src/lib/auth/requireAuth.ts†L74-L119】`
- Admin layout redirects non-admin users away from `/admin/*`. `【F:web/src/layouts/admin/Layout.tsx†L11-L18】`
- The public/group selector UI changes what can be edited based on the current role. `【F:web/src/components/IsPublicGroupSelector.tsx†L33-L124】`

## Backend admin enforcement
- Backend route dependencies remain the authoritative control point for admin access. `【F:backend/onyx/auth/permissions.py†L101-L127】`
- `get_current_user_permissions()` exposes the effective permission set rather than relying on the frontend. `【F:backend/onyx/server/manage/users.py†L872-L876】`

## Gaps and unverified areas
- No runtime route-matrix validation was performed.
- No live user-role mutation flow was exercised.
- No exhaustive check was performed for every curator-sensitive endpoint.
- Frontend gating exists, but backend enforcement still needs runtime validation.
