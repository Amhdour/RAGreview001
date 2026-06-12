# PHASE 5 Authorization Flow Map

## 1. Purpose
This map identifies role, permission, group, token-scope, tenant, admin-gate, and frontend UI-gating evidence in repository files.

## 2. Scope
- In scope: `backend/onyx/auth/permissions.py`, `backend/onyx/auth/users.py`, `backend/onyx/server/auth_check.py`, `backend/onyx/db/enums.py`, `backend/onyx/db/models.py`, authorization-relevant route files under `backend/onyx/server/`, Enterprise DB authorization helpers under `backend/ee/onyx/db/`, shared tenant files under `shared_configs/`, and frontend admin/permission routing files under `web/src/`.
- Out of scope: live group membership, live tenant assignments, external IdP authorization rules, and manual admin procedures not represented in repository files.

## 3. Main entry points
- Permission dependency factory and effective-permission logic: `backend/onyx/auth/permissions.py`.
- Current-user and token-scope handling: `backend/onyx/auth/users.py`.
- Route auth verification helper: `backend/onyx/server/auth_check.py`.
- Permission enum: `backend/onyx/db/enums.py`.
- User, group, permission, connector, document-set, credential, persona, and MCP relationship models: `backend/onyx/db/models.py`.
- Admin/security route examples: `backend/onyx/server/security/api.py`, `backend/onyx/server/manage/users.py`, `backend/onyx/server/features/persona/api.py`, `backend/onyx/server/features/tool/api.py`, `backend/onyx/server/features/mcp/api.py`.
- Tenant context/config: `backend/shared_configs/contextvars.py`, `backend/shared_configs/configs.py`, `backend/onyx/utils/tenant.py`.
- Frontend admin route metadata and permission-aware UI code: `web/src/lib/admin-routes.ts`, `web/src/sections/modals/languageModels/shared.tsx`.

## 4. Architecture flow
1. `backend/onyx/db/enums.py` defines permission enum values.
2. `backend/onyx/db/models.py` defines users, user groups, permission grants, and relationship tables that connect users/groups to documents, document sets, credentials, skills, personas, tools/MCP, and LLM providers.
3. `backend/onyx/auth/permissions.py` expands implied permissions and exposes `require_permission()` as a FastAPI dependency factory.
4. Route files apply authorization by using user dependencies or `require_permission()` dependencies.
5. `backend/onyx/server/auth_check.py` inspects routes for auth dependencies, which is evidence of route-level auth coverage checking.
6. Tenant context is represented by shared context/config files and backend tenant utility modules.
7. Frontend route/menu gating evidence is represented by admin route metadata and UI code that references roles or agents/groups.

## 5. Supporting evidence
- `backend/onyx/auth/permissions.py` — permission implication map, effective permission calculation, `require_permission()` dependency.
- `backend/onyx/auth/users.py` — current-user dependencies and token-scope logic.
- `backend/onyx/server/auth_check.py` — route dependency inspection for auth coverage.
- `backend/onyx/db/enums.py` — `Permission` enum and other auth-related enums.
- `backend/onyx/db/models.py` — `User`, `UserGroup`, `PermissionGrant`, relationship models, and scoped domain entities.
- `backend/onyx/server/security/api.py` — route file using full-admin permission dependency.
- `backend/onyx/server/manage/users.py` — user/admin management routes.
- `backend/onyx/server/features/persona/api.py`, `backend/onyx/server/features/tool/api.py`, `backend/onyx/server/features/mcp/api.py` — feature routes where permission checks can be reviewed.
- `backend/shared_configs/contextvars.py`, `backend/shared_configs/configs.py`, `backend/onyx/utils/tenant.py` — tenant context/config evidence.
- `web/src/lib/admin-routes.ts`, `web/src/sections/modals/languageModels/shared.tsx` — frontend admin/role-aware UI evidence.

## 6. Dependencies
- Internal dependencies: authorization code depends on DB enum/model definitions, current-user dependencies, route modules, and tenant context helpers.
- External dependencies supported by files: none required to state authorization architecture; live IdP/group sync integrations require deeper review of connector/auth integration files.

## 7. Gaps / unknowns
- Actual user memberships, tenant assignments, and live permission grants are runtime data and are not known from source files.
- A complete per-route authorization matrix requires deeper handler-by-handler review.

## 8. Client-ready summary
Authorization is modeled through users, roles, permission enums, user groups, relationship tables, token scopes, and FastAPI dependencies. Backend route files can require specific permissions. Frontend admin navigation and role-aware screens provide UI-level gating, but backend permission checks are the authoritative evidence for authorization behavior.

## Support table
| Claim | Evidence file paths | Support status | Notes |
|---|---|---:|---|
| Permissions are modeled as enum values and expanded through backend logic. | `backend/onyx/db/enums.py`, `backend/onyx/auth/permissions.py` | Supported | Permission enum and implication map exist. |
| Route handlers can require permissions through a FastAPI dependency. | `backend/onyx/auth/permissions.py`, `backend/onyx/server/security/api.py` | Supported | `require_permission()` and full-admin route dependency evidence exist. |
| Users, groups, permission grants, and domain relationships are persisted models. | `backend/onyx/db/models.py` | Supported | Model classes include users, user groups, permission grants, and join tables. |
| Token scopes participate in permission decisions. | `backend/onyx/auth/users.py`, `backend/onyx/auth/permissions.py` | Supported | Auth and permission files reference token scope handling. |
| Tenant context has source-level support. | `backend/shared_configs/contextvars.py`, `backend/shared_configs/configs.py`, `backend/onyx/utils/tenant.py` | Supported | Tenant context/config utility files exist. |
| Frontend admin route/UI gating is represented in source files. | `web/src/lib/admin-routes.ts`, `web/src/sections/modals/languageModels/shared.tsx` | Supported | Admin metadata and role/agent/group-aware UI files exist. |
| Actual live user permissions are known. | No repository evidence identified. | Unsupported | Live permissions are runtime database state. |

## Missing or unsupported items
- Live user/group permissions and a complete per-route authorization matrix are unsupported without runtime data and a deeper route audit.
