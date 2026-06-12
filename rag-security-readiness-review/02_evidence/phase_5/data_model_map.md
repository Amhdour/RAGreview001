# PHASE 5 Data Model Map

## 1. Purpose
This map identifies persistent data model definitions, migration evidence, database helper modules, and Enterprise Edition database extensions.

## 2. Scope
- In scope: `backend/onyx/db/`, `backend/alembic/`, `backend/alembic_tenants/`, and `backend/ee/onyx/db/`.
- Out of scope: live database contents, generated database schema after migration execution, and external warehouse/analytics stores not represented by repository files.

## 3. Main entry points
- SQLAlchemy model definitions: `backend/onyx/db/models.py`.
- Enum definitions: `backend/onyx/db/enums.py`.
- Database engine/session helpers: `backend/onyx/db/engine/`.
- Domain-specific DB helpers: `backend/onyx/db/auth.py`, `backend/onyx/db/users.py`, `backend/onyx/db/connector.py`, `backend/onyx/db/credentials.py`, `backend/onyx/db/document.py`, `backend/onyx/db/chat.py`, `backend/onyx/db/persona.py`, `backend/onyx/db/tools.py`, `backend/onyx/db/mcp.py`, and peer files under `backend/onyx/db/`.
- Alembic migrations: `backend/alembic/` and `backend/alembic/versions/`.
- Tenant migrations: `backend/alembic_tenants/`.
- Enterprise DB helpers: `backend/ee/onyx/db/`.

## 4. Architecture flow
1. Persistent entity classes are declared in `backend/onyx/db/models.py`.
2. Model enums and status/type values are declared in `backend/onyx/db/enums.py`.
3. Domain-specific modules in `backend/onyx/db/` provide data access operations for auth, users, connectors, credentials, documents, chat, personas, tools, MCP, search settings, and other domains.
4. Schema migrations are stored under `backend/alembic/versions/`.
5. Tenant-specific migration support is represented under `backend/alembic_tenants/`.
6. Enterprise Edition database helpers are separated under `backend/ee/onyx/db/`.

## 5. Supporting evidence
- `backend/onyx/db/models.py` — persistent model classes including users, API keys, PATs, connectors, credentials, documents, index attempts, chat sessions/messages, LLM providers, tools, personas, user groups, MCP servers/configs, build sessions, scheduled tasks, SCIM, hooks, and external apps.
- `backend/onyx/db/enums.py` — enum classes for account type, permissions, indexing status, MCP transport/auth/status, chat sharing, build/sandbox status, scheduled task status, PAT type, and related state values.
- `backend/onyx/db/engine/` — SQLAlchemy engine/session helpers.
- `backend/onyx/db/auth.py`, `backend/onyx/db/users.py`, `backend/onyx/db/document.py`, `backend/onyx/db/chat.py`, `backend/onyx/db/mcp.py` — examples of domain-specific database operations.
- `backend/alembic/versions/` — migration scripts for schema evolution.
- `backend/alembic_tenants/` — tenant migration area.
- `backend/ee/onyx/db/` — Enterprise Edition DB helper modules for analytics, connectors, documents, document sets, external permissions, hierarchy, license, query history, SAML, SCIM, search, standard answers, token limits, usage export, and user groups.

## 6. Dependencies
- Internal dependencies: API, auth, connector, indexing, chat, MCP, and management modules depend on DB models/helpers.
- External infrastructure dependencies supported by files: SQLAlchemy is used for ORM/database access in `backend/onyx/db/models.py` and engine helpers; Alembic migration directories represent relational schema migration support.

## 7. Gaps / unknowns
- The exact live database schema depends on which migrations have been applied; this map does not claim runtime migration state.
- Table sizes, row counts, and production data quality are unknown from source files.

## 8. Client-ready summary
The repository centralizes persistent data definitions in one large SQLAlchemy models file, supported by domain-specific database helper modules. Schema changes are tracked with Alembic migrations. Enterprise Edition database behavior is separated into its own backend directory.

## Support table
| Claim | Evidence file paths | Support status | Notes |
|---|---|---:|---|
| Persistent entities are defined with SQLAlchemy models. | `backend/onyx/db/models.py` | Supported | The file declares many `Base` model classes. |
| Enum/state values are defined separately from models. | `backend/onyx/db/enums.py` | Supported | The file declares permission, status, and type enums. |
| Domain-specific DB operations are grouped under `backend/onyx/db/`. | `backend/onyx/db/auth.py`, `backend/onyx/db/users.py`, `backend/onyx/db/document.py`, `backend/onyx/db/chat.py`, `backend/onyx/db/mcp.py` | Supported | Helper modules are organized by domain. |
| Schema migration evidence exists. | `backend/alembic/`, `backend/alembic/versions/` | Supported | Alembic migration directories are present. |
| Tenant migration evidence exists. | `backend/alembic_tenants/` | Supported | Tenant migration directory is present. |
| Enterprise Edition DB helpers are separate. | `backend/ee/onyx/db/` | Supported | EE DB helper modules are present. |
| Current production schema and data contents are known. | No repository evidence identified. | Unsupported | Runtime database state is not in repository files. |

## Missing or unsupported items
- Runtime-applied migration state, table sizes, row counts, and production data contents are unsupported by repository files.
