# Workspace Setup Evidence

## Review phase
PHASE 1 — Prepare the review workspace

## Repository
- Name: RAGreview001
- Path: /workspace/RAGreview001
- Branch: work
- Commit: 3db3b981b78b8184e3a61695f8cafd6def4c8cd3

## Date/time
2026-06-10T18:28:55Z

## Reviewer
Codex

## Confirmed facts
- Repository root confirmed at `/workspace/RAGreview001`.
- Repository name recorded as `RAGreview001`.
- Current branch recorded as `work`.
- Current commit recorded as `3db3b981b78b8184e3a61695f8cafd6def4c8cd3`.
- Captured environment timestamp: `2026-06-10T18:28:55Z`.
- Reviewer name recorded from git configuration as `Codex`.
- Machine OS recorded as `Linux c82174dc2c50 6.12.47 #1 SMP Mon Oct 27 10:01:15 UTC 2025 x86_64 x86_64 x86_64 GNU/Linux`.
- Python version recorded as `Python 3.13.13`.
- Node version recorded as `v24.15.0`.
- npm version recorded as `11.4.2`.
- pnpm version recorded as `NOT AVAILABLE`.
- yarn version recorded as `NOT AVAILABLE`.
- Docker version recorded as `NOT AVAILABLE`.
- Git version recorded as `git version 2.43.0`.
- Workspace root created at `rag-security-readiness-review/` with the requested subdirectory layout.
- Source snapshots created in `00_original_source/` and `01_working_copy/`.
- Workspace tree captured to `02_evidence/raw_outputs/workspace_tree.txt`.
- The workspace directories required by the task were created.
- The original source snapshot was preserved in `00_original_source/`.
- The working copy snapshot was created in `01_working_copy/`.


## Assumptions
- The repository snapshot used for copying represents the current source state at the time of setup.
- Source snapshots intentionally exclude the workspace directory itself to avoid recursive copying.
- Generated artifacts, caches, virtual environments, and secret-bearing `.env` files were intentionally not mirrored into the copies.
- `UNCONFIRMED` is reserved for values that could not be directly verified.
- `NOT AVAILABLE` is reserved for tools that are missing or could not return a usable version.


## Limitations
- The source copies are filesystem snapshots, not standalone git repositories.
- The workspace tree output is a filesystem listing created after the copy step and is not a cryptographic attestation.
- Docker was not available in the environment, so a Docker version could not be confirmed.
- pnpm and yarn version checks were not available as standalone tools in this environment.
- This phase does not validate application security controls, functionality, or production readiness.


## Commands executed
1. `pwd`
2. `rg --files -g 'AGENTS.md' -g 'CONTRIBUTING.md' -g '.git' -g '.env' -g 'pyproject.toml' -g 'package.json' /workspace/RAGreview001 /workspace 2>/dev/null | sed 's#^#FOUND #'`
3. `sed -n '1,260p' AGENTS.md && printf '
--- CONTRIBUTING ---
' && sed -n '1,260p' CONTRIBUTING.md`
4. `set -euo pipefail; ROOT=$(git rev-parse --show-toplevel); BRANCH=$(git branch --show-current || true); COMMIT=$(git rev-parse HEAD); REPO_NAME=$(basename "$ROOT"); REPO_PATH=$ROOT; NOW_UTC=$(date -u '+%Y-%m-%dT%H:%M:%SZ'); REVIEWER=$(git config --get user.name || true); OS_INFO=$(uname -a); PYTHON_VERSION=$(python --version 2>&1 || true); NODE_VERSION=$(node --version 2>&1 || true); NPM_VERSION=$(npm --version 2>&1 || true); PNPM_VERSION=$(pnpm --version 2>&1 || true); YARN_VERSION=$(yarn --version 2>&1 || true); DOCKER_VERSION=$(docker --version 2>&1 || true); GIT_VERSION=$(git --version 2>&1 || true); printf 'ROOT=%s
BRANCH=%s
COMMIT=%s
REPO_NAME=%s
NOW_UTC=%s
REVIEWER=%s
OS=%s
PY=%s
NODE=%s
NPM=%s
PNPM=%s
YARN=%s
DOCKER=%s
GIT=%s
' "$REPO_PATH" "${BRANCH:-UNCONFIRMED}" "$COMMIT" "$REPO_NAME" "$NOW_UTC" "${REVIEWER:-Ahmed / Mervan Karageçi}" "$OS_INFO" "$PYTHON_VERSION" "$NODE_VERSION" "${NPM_VERSION:-NOT AVAILABLE}" "${PNPM_VERSION:-NOT AVAILABLE}" "${YARN_VERSION:-NOT AVAILABLE}" "${DOCKER_VERSION:-NOT AVAILABLE}" "$GIT_VERSION"`
5. `set -euo pipefail; ROOT=$(git rev-parse --show-toplevel); WS="$ROOT/rag-security-readiness-review"; mkdir -p "$WS/00_original_source" "$WS/01_working_copy" "$WS/02_evidence/environment" "$WS/02_evidence/inventory" "$WS/02_evidence/commands" "$WS/02_evidence/screenshots" "$WS/02_evidence/raw_outputs" "$WS/03_reports" "$WS/04_public_case_study" "$WS/05_scripts" "$WS/06_templates"; rsync -a --delete --exclude 'rag-security-readiness-review/' --exclude '\.git/' --exclude '\.venv/' --exclude 'node_modules/' --exclude '\.next/' --exclude 'dist/' --exclude 'build/' --exclude 'coverage/' --exclude '__pycache__/' --exclude '\.pytest_cache/' --exclude '\.mypy_cache/' --exclude '\.ruff_cache/' --exclude '\.env' --exclude '\.env.*' "$ROOT/" "$WS/00_original_source/"; rsync -a --delete --exclude 'rag-security-readiness-review/' --exclude '\.git/' --exclude '\.venv/' --exclude 'node_modules/' --exclude '\.next/' --exclude 'dist/' --exclude 'build/' --exclude 'coverage/' --exclude '__pycache__/' --exclude '\.pytest_cache/' --exclude '\.mypy_cache/' --exclude '\.ruff_cache/' --exclude '\.env' --exclude '\.env.*' "$ROOT/" "$WS/01_working_copy/"; find "$WS" -maxdepth 3 -print | sort > "$WS/02_evidence/raw_outputs/workspace_tree.txt"`
6. `python - <<'PY' ...` — failed once with `KeyError: 'WS'` because the Python process did not receive exported shell variables; the command was rerun successfully after exporting them.


## Evidence created
- `rag-security-readiness-review/README.md`
- `rag-security-readiness-review/02_evidence/workspace_setup.md`
- `rag-security-readiness-review/02_evidence/environment/environment_record.md`
- `rag-security-readiness-review/02_evidence/review_metadata.md`
- `rag-security-readiness-review/02_evidence/assumptions.md`
- `rag-security-readiness-review/02_evidence/commands/commands_executed.md`
- `rag-security-readiness-review/02_evidence/raw_outputs/workspace_tree.txt`
- `rag-security-readiness-review/03_reports/phase_1_workspace_setup_report.md`
- `rag-security-readiness-review/06_templates/workspace_setup.md`
- `rag-security-readiness-review/06_templates/environment_record.md`
- `rag-security-readiness-review/06_templates/review_metadata.md`
- `rag-security-readiness-review/06_templates/assumptions.md`


## Missing evidence
- No additional missing evidence was identified for PHASE 1 beyond unavailable tooling checks recorded as `NOT AVAILABLE`.


## Next step
PHASE 2 — Establish review boundaries
