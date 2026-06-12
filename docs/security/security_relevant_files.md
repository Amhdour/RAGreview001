> This is the client-facing mirror of the PHASE 3 evidence file. The canonical evidence copy remains under rag-security-readiness-review/02_evidence/phase_3/.

# PHASE 3 Security Relevant Files

## Authentication

### Confirmed files
- `backend/onyx/auth/jwt.py`
- `backend/onyx/auth/oauth_token_manager.py`
- `backend/onyx/server/auth/captcha_api.py`
- `web/src/app/auth/login/EmailPasswordForm.tsx`
- `mobile/src/api/auth/tokenStore.ts`

### Candidate files
- `backend/alembic/versions/2666d766cb9b_google_oauth2.py`
- `backend/onyx/server/features/oauth_config/api.py`
- `backend/ee/onyx/server/oauth/api.py`

### Why relevant
These paths govern login, token issuance/storage, and auth-related APIs.

### Inventory limitation
File-name matching only; no runtime flow validation.

### Next review phase
PHASE 4 — Separate original vs added work

## Authorization and permissions

### Confirmed files
- `backend/onyx/auth/permissions.py`
- `backend/ee/onyx/external_permissions/google_drive/permission_retrieval.py`
- `backend/ee/onyx/external_permissions/sharepoint/permission_utils.py`
- `backend/ee/onyx/external_permissions/slack/channel_access.py`

### Candidate files
- `backend/ee/onyx/external_permissions/confluence/group_sync.py`
- `backend/ee/onyx/external_permissions/github/group_sync.py`
- `backend/onyx/server/features/projects/api.py`

### Why relevant
These paths reflect access-control logic, group sync, and permission propagation.

### Inventory limitation
File-name matching only; no effective-permission verification.

### Next review phase
PHASE 4 — Separate original vs added work

## RAG/retrieval

### Confirmed files
- `backend/onyx/document_index/vespa/chunk_retrieval.py`
- `backend/onyx/document_index/vespa/vespa_document_index.py`
- `backend/onyx/document_index/opensearch/search.py`
- `backend/onyx/chat/citation_utils.py`
- `backend/onyx/server/features/search/api.py`
- `web/src/components/search/results/Citation.tsx`

### Candidate files
- `backend/onyx/prompts/contextual_retrieval.py`
- `backend/onyx/secondary_llm_flows/query_expansion.py`
- `backend/ee/onyx/prompts/query_expansion.py`

### Why relevant
These paths indicate retrieval, indexing, citation, and query-expansion surfaces.

### Inventory limitation
File-name matching only; no retrieval-quality or citation-integrity testing.

### Next review phase
PHASE 4 — Separate original vs added work

## Document ingestion

### Confirmed files
- `backend/onyx/connectors/factory.py`
- `backend/onyx/connectors/mock_connector/connector.py`
- `backend/onyx/indexing/chunking/document_chunker.py`
- `backend/onyx/file_processing/extract_file_text.py`
- `backend/onyx/server/documents/document.py`

### Candidate files
- `backend/ee/onyx/external_permissions/google_drive/doc_sync.py`
- `backend/ee/onyx/external_permissions/sharepoint/doc_sync.py`
- `backend/ee/onyx/external_permissions/slack/doc_sync.py`

### Why relevant
These paths indicate ingestion, parsing, syncing, and document preparation.

### Inventory limitation
File-name matching only; no live ingestion validation.

### Next review phase
PHASE 4 — Separate original vs added work

## Prompt-construction exposure

### Confirmed files
- `backend/onyx/prompts/contextual_retrieval.py`
- `backend/ee/onyx/prompts/query_expansion.py`
- `backend/onyx/secondary_llm_flows/query_expansion.py`
- `backend/onyx/chat/citation_processor.py`

### Candidate files
- `backend/onyx/document_index/chunk_content_enrichment.py`
- `backend/onyx/server/query_and_chat/chat_utils.py`
- `backend/ee/onyx/server/query_and_chat/search_backend.py`

### Why relevant
These paths may influence prompt assembly, query expansion, and retrieved-context shaping.

### Inventory limitation
File-name matching only; no prompt-output inspection.

### Next review phase
PHASE 4 — Separate original vs added work

## Citation/source integrity

### Confirmed files
- `backend/onyx/chat/citation_processor.py`
- `backend/onyx/chat/citation_utils.py`
- `web/src/components/search/results/Citation.tsx`
- `backend/onyx/document_index/vespa/chunk_retrieval.py`

### Candidate files
- `backend/onyx/document_index/chunk_content_enrichment.py`
- `backend/onyx/server/features/search/api.py`
- `backend/ee/onyx/server/query_and_chat/query_backend.py`

### Why relevant
These paths likely shape how sources are attached, rendered, or preserved.

### Inventory limitation
File-name matching only; no citation correctness check.

### Next review phase
PHASE 4 — Separate original vs added work

## Connectors

### Confirmed files
- `backend/onyx/connectors/factory.py`
- `backend/onyx/connectors/mock_connector/connector.py`
- `backend/onyx/connectors/credentials_provider.py`
- `backend/onyx/server/documents/connector.py`

### Candidate files
- `backend/ee/onyx/external_permissions/github/doc_sync.py`
- `backend/ee/onyx/external_permissions/google_drive/doc_sync.py`
- `backend/ee/onyx/external_permissions/slack/doc_sync.py`

### Why relevant
These paths expose connector registration, credentials, and document-source integration.

### Inventory limitation
File-name matching only; no connector execution.

### Next review phase
PHASE 4 — Separate original vs added work

## Agent/tool behavior

### Confirmed files
- `backend/onyx/coding_agent/mock_tools.py`
- `backend/onyx/server/features/tool/api.py`
- `backend/onyx/server/manage/code_interpreter/api.py`
- `backend/onyx/server/manage/image_generation/api.py`
- `web/src/app/admin/actions/page.tsx`

### Candidate files
- `backend/onyx/server/features/skill/api.py`
- `backend/onyx/server/features/mcp/api.py`
- `web/src/app/admin/agents/page.tsx`

### Why relevant
These paths point to tool registration, admin action surfaces, and agent-adjacent behavior.

### Inventory limitation
File-name matching only; no tool execution or approval-flow validation.

### Next review phase
PHASE 4 — Separate original vs added work

## MCP

### Confirmed files
- `.mcp.json`
- `backend/onyx/mcp_server_main.py`
- `backend/onyx/mcp_server/api.py`
- `backend/onyx/mcp_server/auth.py`
- `backend/onyx/server/features/mcp/api.py`
- `backend/onyx/db/mcp.py`

### Candidate files
- `backend/onyx/mcp_server/mcp.json.template`
- `backend/tests/external_dependency_unit/server/features/mcp/test_per_user_api_token_credentials.py`

### Why relevant
These paths indicate MCP configuration, auth, and server-side support.

### Inventory limitation
File-name matching only; no protocol interaction testing.

### Next review phase
PHASE 4 — Separate original vs added work

## Sandbox/file handling

### Confirmed files
- `backend/onyx/sandbox_proxy/server.py`
- `backend/onyx/sandbox_proxy/credential_injection.py`
- `backend/onyx/sandbox_proxy/request_evaluator.py`
- `backend/onyx/file_processing/file_types.py`
- `backend/onyx/file_processing/password_validation.py`

### Candidate files
- `backend/onyx/sandbox_proxy/approval_cache.py`
- `backend/onyx/sandbox_proxy/snapshot_egress.py`
- `backend/onyx/file_processing/extract_file_text.py`

### Why relevant
These paths show sandboxing, credential injection, and file handling controls.

### Inventory limitation
File-name matching only; no file-safety or sandbox-evasion testing.

### Next review phase
PHASE 4 — Separate original vs added work

## Secrets and credentials

### Confirmed files
- `.vscode/.env.k8s.template`
- `.vscode/env_template.txt`
- `backend/onyx/auth/jwt.py`
- `backend/onyx/db/credentials.py`
- `backend/onyx/external_apps/credentials.py`
- `backend/onyx/sandbox_proxy/credential_injection.py`

### Candidate files
- `backend/onyx/server/documents/credential.py`
- `backend/onyx/connectors/credentials_provider.py`
- `backend/tests/external_dependency_unit/craft/test_credential_encryption.py`

### Why relevant
These paths indicate credential storage, template handling, and injection points.

### Inventory limitation
File-name matching only; no secret exposure analysis.

### Next review phase
PHASE 4 — Separate original vs added work

## Logging and telemetry

### Confirmed files
- `backend/onyx/tracing/flows.py`
- `backend/onyx/tracing/setup.py`
- `backend/onyx/server/metrics/metrics_server.py`
- `backend/ee/onyx/utils/telemetry.py`
- `backend/onyx/background/celery/tasks/monitoring/tasks.py`

### Candidate files
- `backend/onyx/tracing/langfuse_tracing_processor.py`
- `backend/onyx/tracing/braintrust_tracing_processor.py`
- `backend/onyx/server/metrics/indexing_pipeline.py`

### Why relevant
These paths indicate metrics, tracing, monitoring, and telemetry reporting.

### Inventory limitation
File-name matching only; no operational observability verification.

### Next review phase
PHASE 4 — Separate original vs added work

## CI/CD

### Confirmed files
- `.pre-commit-config.yaml`
- `Makefile`
- `backend/.trivyignore`
- `backend/Dockerfile`
- `cli/pyproject.toml`
- `backend/uv.lock`

### Candidate files
- `.devcontainer/devcontainer.json`
- `.vscode/launch.json`
- `backend/.gitignore`

### Why relevant
These paths indicate build, lint, scanning, and automation configuration.

### Inventory limitation
File-name matching only; no pipeline execution.

### Next review phase
PHASE 4 — Separate original vs added work

## Supply chain

### Confirmed files
- `pyproject.toml`
- `backend/uv.lock`
- `cli/go.mod`
- `cli/go.sum`
- `desktop/src-tauri/Cargo.toml`
- `desktop/src-tauri/Cargo.lock`

### Candidate files
- `bun.lock`
- `mobile/bun.lock`
- `.pre-commit-config.yaml`
- `backend/.trivyignore`

### Why relevant
These files shape dependency resolution, lock states, and pre-commit or scan controls.

### Inventory limitation
File-name matching only; no SBOM or vulnerability scan execution.

### Next review phase
PHASE 4 — Separate original vs added work

## Deployment

### Confirmed files
- `backend/Dockerfile`
- `backend/Dockerfile.model_server`
- `deployment/docker_compose/docker-compose.yml`
- `deployment/docker_compose/docker-compose.prod.yml`
- `deployment/helm/README.md`
- `deployment/terraform/modules/aws/onyx/main.tf`
- `.devcontainer/Dockerfile`
- `docker-bake.hcl`

### Candidate files
- `deployment/docker_compose/env.template`
- `deployment/docker_compose/install.sh`
- `deployment/helm/dev/k8s-up.sh`

### Why relevant
These paths indicate container, compose, Helm, Terraform, and local environment deployment surfaces.

### Inventory limitation
File-name matching only; no deployment execution.

### Next review phase
PHASE 4 — Separate original vs added work

## Tests

### Confirmed files
- `backend/tests/integration/tests/security/test_runtime_security_settings.py`
- `backend/tests/integration/tests/permissions/test_auth_permission_propagation.py`
- `backend/tests/unit/onyx/chat/test_citation_utils.py`
- `web/tests/e2e/auth/password_managements.spec.ts`
- `backend/tests/external_dependency_unit/server/security/test_security_settings_put.py`

### Candidate files
- `backend/tests/unit/onyx/document_index/opensearch/test_get_doc_chunk_id.py`
- `backend/tests/integration/tests/query_history/test_query_history.py`
- `backend/tests/daily/embedding/test_embeddings.py`

### Why relevant
These paths indicate unit, integration, external-dependency, and E2E coverage areas.

### Inventory limitation
File-name matching only; no tests were run in this phase.

### Next review phase
PHASE 4 — Separate original vs added work
