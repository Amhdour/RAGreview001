# PHASE 10 Control Gap Analysis Commands Executed

No application tests, CI jobs, or exploit tests were executed.

| Command | Purpose | Result |
| --- | --- | --- |
| `pwd` | Confirm working directory. | `/workspace/RAGreview001` |
| `git rev-parse --show-toplevel` | Confirm repository root. | `/workspace/RAGreview001` |
| `git branch --show-current` | Confirm branch. | `work` |
| `git rev-parse HEAD` | Record current checkout commit. | `d53d3c0bb614f8a50b72185ee98ab9c1960f757c` |
| `git status --short` | Inspect current working tree before changes. | No output before PHASE 10 writes; working tree appeared clean. |
| `test -f rag-security-readiness-review/03_reports/phase_8_risk_to_code_mapping_report.md && echo EXISTS || echo NOT_AVAILABLE` | Check PHASE 8 report availability. | `EXISTS` |
| `test -f rag-security-readiness-review/03_reports/phase_9_control_to_test_mapping_report.md && echo EXISTS || echo NOT_AVAILABLE` | Check PHASE 9 report availability. | `EXISTS` |
| `test -f rag-security-readiness-review/03_reports/phase_10a_authorization_review_report.md && echo EXISTS || echo NOT_AVAILABLE` | Check PHASE 10A report availability. | `EXISTS` |
| `find rag-security-readiness-review/02_evidence/phase_8 -maxdepth 2 -type f | sort` | Inventory PHASE 8 files. | Completed. |
| `find rag-security-readiness-review/02_evidence/phase_9 -maxdepth 3 -type f | sort` | Inventory PHASE 9 files. | Completed. |
| `find rag-security-readiness-review/02_evidence/phase_10/authorization_review -maxdepth 3 -type f | sort` | Inventory PHASE 10A authorization files. | Completed. |
| `find docs/security -maxdepth 2 -type f | sort` | Inventory docs/security files. | Completed. |
| `rg -n -i "EXISTING-CANDIDATE|MISSING-CANDIDATE|UNVERIFIED|control|candidate|risk|threat|missing|partial|evidence|test" rag-security-readiness-review/02_evidence/phase_8 rag-security-readiness-review/02_evidence/phase_9 rag-security-readiness-review/02_evidence/phase_10/authorization_review docs/security 2>/dev/null || true` | Review candidate/evidence language in prior phases. | Completed. |
| `cat AGENTS.md` | Read repository instructions. | Completed. |
| `cat` / `sed` / `nl` read commands for PHASE 8/9/10A files | Review required evidence files. | Completed. |
| `python - <<'PY' ... PY` | Generate PHASE 10 evidence, raw outputs, templates, mirrors, report, and command log. | Completed. |
| `for f in docs/security/...; do head -n 1 "$f"; done` | Verify PHASE 10 docs/security mirror preamble. | Completed; each mirror began with the required preamble. |
| `find rag-security-readiness-review/02_evidence/phase_10 -maxdepth 2 -type f | sort` | Verify PHASE 10 canonical and raw files. | Completed. |
| `find rag-security-readiness-review/06_templates/phase_10 -maxdepth 1 -type f | sort` | Verify PHASE 10 templates. | Completed. |
| `python - <<'PY' ... PY` | Check required PHASE 10 file paths exist. | Completed; no missing paths reported. |
| `rg -n "\b(VALIDATED|PASSED|EFFECTIVE|validated control|tests passed|CI passed|production readiness|exploitability)\b" ... || true` | Review non-claim wording in generated PHASE 10 files. | Completed; hits were non-claim/limitation wording rather than validation claims. |
| `git diff --check` | Check generated markdown for whitespace errors. | Completed with no output. |

## Skipped commands
- Application tests were skipped by instruction.
- CI was skipped by instruction.
- Exploit tests were skipped by instruction.
- Runtime service checks were skipped because PHASE 10 is source-only.
