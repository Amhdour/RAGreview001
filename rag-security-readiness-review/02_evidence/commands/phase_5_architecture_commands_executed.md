# PHASE 5 Architecture Commands Executed

## Purpose
Record the repository commands used to read the existing PHASE 5 architecture maps and produce the strict evidence package.

## Commands executed
1.
   ```bash
   pwd && rg --files -g 'AGENTS.md' -g 'rag-security-readiness-review/**' -g 'docs/security/**' | sed 's#^#/#' | head -n 200
   ```
2.
   ```bash
   sed -n '1,220p' AGENTS.md && printf '\n--- PHASE5 ARCH MAP ---\n' && sed -n '1,220p' rag-security-readiness-review/02_evidence/phase_5/architecture_map.md && printf '\n--- BACKEND ---\n' && sed -n '1,240p' rag-security-readiness-review/02_evidence/phase_5/backend_architecture.md && printf '\n--- FRONTEND ---\n' && sed -n '1,240p' rag-security-readiness-review/02_evidence/phase_5/frontend_architecture.md && printf '\n--- API ROUTES ---\n' && sed -n '1,260p' rag-security-readiness-review/02_evidence/phase_5/api_routes_map.md
   ```
3.
   ```bash
   echo '--- phase_4 index ---' && sed -n '1,220p' docs/security/phase_4_original_vs_added_index.md && echo '\n--- phase_3 important files index ---' && sed -n '1,220p' docs/security/important_files_index.md && echo '\n--- phase_5 commands ---' && sed -n '1,260p' rag-security-readiness-review/02_evidence/commands/phase_5_commands_executed.md && echo '\n--- phase_5 summary existing? ---' && sed -n '1,260p' rag-security-readiness-review/02_evidence/phase_5/phase_5_summary.md
   ```
4.
   ```bash
   echo '--- phase_4 templates ---' && for f in rag-security-readiness-review/06_templates/phase_4/*; do echo "===== $f ====="; sed -n '1,220p' "$f"; echo; done && echo '--- phase_3 templates ---' && for f in rag-security-readiness-review/06_templates/phase_3/*; do echo "===== $f ====="; sed -n '1,220p' "$f"; echo; done
   ```
5.
   ```bash
   python - <<'PY' ... PY
   ```

## Commands intentionally not run
- Runtime application validation commands: not run for this strict evidence-only phase.
- Security or exploit tests: not run.
- Unit, integration, E2E, or CI jobs: not run.
