# PHASE 5 Raw Architecture Evidence Commands

## Purpose
Record the read-only file-search commands used to generate PHASE 5 raw architecture evidence outputs.

## Output directory
`rag-security-readiness-review/02_evidence/phase_5/raw_outputs/`

## Commands executed
1. `backend_architecture_file_search.txt`

   ```bash
   rg --files backend -g '!**/.venv/**' -g '!**/node_modules/**' -g '!**/.next/**' -g '!**/__pycache__/**' | rg '(^backend/(onyx|ee|background|alembic|scripts|tests)|Dockerfile|pyproject|requirements|uv\.lock)' | sort
   ```
   Exit code: `0`

2. `frontend_architecture_file_search.txt`

   ```bash
   rg --files web desktop -g '!**/.venv/**' -g '!**/node_modules/**' -g '!**/.next/**' -g '!**/__pycache__/**' 2>/dev/null | rg '(^web/src/(app|components|lib|sections|layouts|refresh-components|refresh-pages|services|hooks|utils)|^web/(package\.json|next\.config|tsconfig|middleware|tailwind|tests|public)|^desktop/)' | sort
   ```
   Exit code: `0`

3. `api_route_file_search.txt`

   ```bash
   rg --files backend web -g '!**/.venv/**' -g '!**/node_modules/**' -g '!**/.next/**' -g '!**/__pycache__/**' | rg '(^backend/(onyx|ee/onyx)/server/.*\.py$|^web/src/app/api/|route\.(ts|tsx|js|jsx)$)' | sort
   ```
   Exit code: `0`

4. `auth_file_search.txt`

   ```bash
   rg --files backend web -g '!**/.venv/**' -g '!**/node_modules/**' -g '!**/.next/**' -g '!**/__pycache__/**' | rg -i '(auth|oauth|oidc|saml|jwt|session|login|logout|password|api[_-]?key|personal[_-]?access|\bpat\b|credential|token)' | sort
   ```
   Exit code: `0`

5. `authorization_file_search.txt`

   ```bash
   rg --files backend web -g '!**/.venv/**' -g '!**/node_modules/**' -g '!**/.next/**' -g '!**/__pycache__/**' | rg -i '(permission|authorization|authorize|rbac|role|group|tenant|access|acl|grant|scope|policy|visibility|sharing|admin)' | sort
   ```
   Exit code: `0`

6. `data_model_file_search.txt`

   ```bash
   rg --files backend -g '!**/.venv/**' -g '!**/node_modules/**' -g '!**/.next/**' -g '!**/__pycache__/**' | rg '(^backend/(onyx|ee/onyx)/db/|^backend/alembic/|^backend/ee/alembic/|models?\.py$|schema.*\.py$|enums?\.py$)' | sort
   ```
   Exit code: `0`

7. `rag_pipeline_file_search.txt`

   ```bash
   rg --files backend web -g '!**/.venv/**' -g '!**/node_modules/**' -g '!**/.next/**' -g '!**/__pycache__/**' | rg -i '(connector|indexing|index_attempt|document_index|vespa|chunk|embed|embedding|retrieval|search|rerank|query|chat|answer|citation|prompt|llm|kg|knowledge|user_file)' | sort
   ```
   Exit code: `0`

8. `agent_tool_mcp_file_search.txt`

   ```bash
   rg --files backend web -g '!**/.venv/**' -g '!**/node_modules/**' -g '!**/.next/**' -g '!**/__pycache__/**' | rg -i '(agent|tool|tools|mcp|model_context|function_call|functioncall|actions?|workflow)' | sort
   ```
   Exit code: `0`

9. `logging_telemetry_file_search.txt`

   ```bash
   rg --files backend web -g '!**/.venv/**' -g '!**/node_modules/**' -g '!**/.next/**' -g '!**/__pycache__/**' | rg -i '(log|logging|logger|telemetry|trace|tracing|metrics?|monitor|observability|sentry|prometheus|stats|heartbeat|audit)' | sort
   ```
   Exit code: `0`

10. `deployment_file_search.txt`

   ```bash
   rg --files . -g '!**/.venv/**' -g '!**/node_modules/**' -g '!**/.next/**' -g '!**/__pycache__/**' -g '!rag-security-readiness-review/02_evidence/phase_5/raw_outputs/**' | rg -i '(^deployment/|docker|compose|helm|k8s|kubernetes|nginx|supervisord|gunicorn|uvicorn|celery|ecs|fargate|terraform|cloudformation|Dockerfile|Procfile|render|fly\.toml|railway|\.github/workflows)' | sort
   ```
   Exit code: `0`

## Commands intentionally not run
- Runtime application validation commands: not run for this raw evidence collection.
- Security or exploit tests: not run.
- Unit, integration, E2E, or CI jobs: not run.

## Notes
- Commands were limited to repository file/path searches.
- No application source code was modified.
- PHASE 5 status remains COMPLETE WITH LIMITATIONS.
