# PHASE 3 Baseline Inventory

## Review phase
PHASE 3 — Create baseline inventory

## Repository
Amhdour/RAGreview001

## Source input type
GitHub repository workspace

## Inventory target path
UNCONFIRMED — `rag-security-readiness-review/01_working_copy/` was not present in this checkout. The baseline inventory was generated from the current repository tree at `/workspace/RAGreview001` with review-artifact and generated folders excluded.

## Date/time
2026-06-12T02:17:50Z

## Reviewer
Codex

## Prepared by
Codex

## Approved by
UNCONFIRMED

## PHASE 1 dependency
PHASE 1 evidence exists in the repository as workspace setup and review metadata artifacts under `rag-security-readiness-review/02_evidence/`.

## PHASE 2 dependency
PHASE 2 evidence exists in `rag-security-readiness-review/02_evidence/phase_2/` and the corresponding report files.

## Inventory objective
Create a baseline inventory of the observed repository tree and identify files that are likely relevant to security review without claiming control verification.

## Confirmed inventory scope
- Repository source tree observed in this checkout.
- Source and documentation files under the current repository root.
- Metadata, config, code, test, deployment, and documentation paths that were present in the filtered inventory.
- Review-artifact directories were excluded from the raw source inventory.

## Excluded inventory scope
- `.git` internals.
- `.venv`, `node_modules`, cache directories, build outputs, dist outputs, coverage outputs, and other generated folders.
- `rag-security-readiness-review/` review-artifact paths.
- `docs/security/` mirror outputs.
- Any path not observed in the filtered inventory.

## Top-level directory summary
The filtered inventory contained 40 top-level entries and was dominated by `backend` (2718 files), `web` (2014 files), `deployment` (172 files), `docs` (67 files), `tools` (66 files), `cli` (62 files), `desktop` (60 files), and `mobile` (32 files). Smaller top-level areas included `extensions`, `widget`, `examples`, `.devcontainer`, `profiling`, `.vscode`, `.claude`, `.greptile`, and repository-level config files such as `README.md`, `SECURITY.md`, `Makefile`, `pyproject.toml`, and lockfiles.

## Deep inventory summary
The filtered inventory contained 5303 files and 135 second-level directory groupings in the generated summaries. The largest second-level clusters were `web/src` (1246 files), `backend/onyx` (1056 files), `backend/tests` (958 files), `web/lib` (551 files), `backend/alembic` (382 files), `backend/ee` (197 files), `web/tests` (115 files), `deployment/helm` (100 files), `backend/scripts` (71 files), `web/public` (70 files), `tools/ods` (66 files), `docs/craft` (64 files), `desktop/src-tauri` (52 files), `cli/internal` (39 files), and `deployment/terraform` (28 files).

## File category summary table
| Category | Observed count | Representative examples | Status |
| --- | --- | --- | --- |
| README/docs | 162 | `README.md`, `README.zh-CN.md`, `docs/METRICS.md`, `backend/alembic/README.md` | CONFIRMED |
| Security policy/docs | 20 | `SECURITY.md`, `.claude/claude-security-guidance.md` | CONFIRMED |
| Dependency files | 30 | `pyproject.toml`, `backend/uv.lock`, `cli/go.mod`, `desktop/package.json`, `mobile/package.json`, `bun.lock` | CONFIRMED |
| Backend files | 2718 | `backend/onyx/main.py`, `backend/ee/onyx/main.py`, `backend/model_server/main.py`, `backend/onyx/mcp_server_main.py` | CONFIRMED |
| Frontend files | 2014 | `web/src/app/page.tsx`, `web/src/app/layout.tsx`, `mobile/src/app/index.tsx`, `desktop/src-tauri/src/main.rs`, `cli/main.go` | CONFIRMED |
| API routes | 173 | `backend/onyx/server/features/search/api.py`, `backend/onyx/server/features/tool/api.py`, `backend/onyx/server/security/api.py` | CONFIRMED |
| Auth files | 305 | `backend/onyx/auth/jwt.py`, `backend/onyx/auth/oauth_token_manager.py`, `web/src/app/auth/login/EmailPasswordForm.tsx` | CONFIRMED |
| Permission/access files | 579 | `backend/onyx/auth/permissions.py`, `backend/ee/onyx/external_permissions/google_drive/permission_retrieval.py`, `backend/ee/onyx/external_permissions/sharepoint/permission_utils.py` | CONFIRMED |
| RAG/retrieval files | 592 | `backend/onyx/document_index/vespa/chunk_retrieval.py`, `backend/onyx/chat/citation_utils.py`, `web/src/components/search/results/Citation.tsx` | CONFIRMED |
| Ingestion files | 817 | `backend/onyx/connectors/factory.py`, `backend/onyx/file_processing/extract_file_text.py`, `backend/onyx/server/documents/document.py` | CONFIRMED |
| Agent/tool files | 544 | `backend/onyx/coding_agent/mock_tools.py`, `backend/onyx/server/features/tool/api.py`, `web/src/app/admin/actions/page.tsx` | CONFIRMED |
| MCP files | 73 | `.mcp.json`, `backend/onyx/mcp_server_main.py`, `backend/onyx/mcp_server/api.py` | CONFIRMED |
| Sandbox/file files | 291 | `backend/onyx/sandbox_proxy/server.py`, `backend/onyx/file_processing/file_types.py` | CONFIRMED |
| Secrets/config files | 163 | `.vscode/.env.k8s.template`, `backend/onyx/db/credentials.py`, `backend/onyx/sandbox_proxy/credential_injection.py` | CONFIRMED |
| Logging/telemetry files | 241 | `backend/onyx/tracing/flows.py`, `backend/onyx/server/metrics/metrics_server.py`, `backend/ee/onyx/utils/telemetry.py` | CONFIRMED |
| CI/CD files | 88 | `.pre-commit-config.yaml`, `Makefile`, `backend/.trivyignore`, `backend/Dockerfile` | CONFIRMED |
| Docker/deployment files | 259 | `backend/Dockerfile`, `deployment/docker_compose/docker-compose.yml`, `deployment/helm/README.md`, `deployment/terraform/modules/aws/onyx/main.tf` | CONFIRMED |
| Test files | 1192 | `backend/tests/integration/tests/security/test_runtime_security_settings.py`, `web/tests/e2e/auth/password_managements.spec.ts` | CONFIRMED |

## Important files summary
See `important_files_index.md` for the category-by-category index of representative paths that are likely to matter in later review phases.

## Security-relevant files summary
See `security_relevant_files.md` for the security-oriented grouping of confirmed and candidate paths.

## Commands executed
See `inventory_commands.md` and `rag-security-readiness-review/02_evidence/commands/phase_3_inventory_commands_executed.md`.

## Raw outputs created
- `rag-security-readiness-review/02_evidence/phase_3/raw_outputs/top_level_file_tree.txt`
- `rag-security-readiness-review/02_evidence/phase_3/raw_outputs/deep_file_tree.txt`
- `rag-security-readiness-review/02_evidence/phase_3/raw_outputs/all_files.txt`
- `rag-security-readiness-review/02_evidence/phase_3/raw_outputs/directory_summary.txt`
- `rag-security-readiness-review/02_evidence/phase_3/raw_outputs/important_files_raw.txt`
- `rag-security-readiness-review/02_evidence/phase_3/raw_outputs/security_relevant_files_raw.txt`

## Missing evidence
- `rag-security-readiness-review/01_working_copy/` was not present in this checkout.
- Runtime evidence was not collected in this phase.
- Production evidence was not collected in this phase.
- CI execution evidence was not collected in this phase.
- Application test execution evidence was not collected in this phase.

## Limitations
- Source-only and local-workspace-only inventory.
- Snapshot limitation: inventory reflects the repository state observed during this run.
- Generated and cache folders were intentionally excluded.
- File-name matching was used to identify candidate security-relevant areas.
- No runtime or production validation was performed.
- No tests or CI workflows were run.

## Non-claims
- This inventory does not verify any security control.
- This inventory does not prove production readiness.
- This inventory does not prove absence of files or functionality.
- This inventory does not claim CI or tests passed.
- This inventory does not include exploit testing.

## Next phase
PHASE 4 — Separate original vs added work

## PHASE 3 status
COMPLETE WITH LIMITATIONS
