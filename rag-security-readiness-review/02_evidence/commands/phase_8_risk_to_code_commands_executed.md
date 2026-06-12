# PHASE 8 Risk to Code Commands Executed

1. `pwd`
2. `git rev-parse --show-toplevel`
3. `git branch --show-current`
4. `git rev-parse HEAD`
5. `git status --short`
6. `test -f rag-security-readiness-review/03_reports/phase_7_risk_taxonomy_report.md && echo EXISTS || echo NOT_AVAILABLE`
7. `find rag-security-readiness-review/02_evidence/phase_7 -maxdepth 2 -type f | sort`
8. `find rag-security-readiness-review/02_evidence/phase_6 -maxdepth 2 -type f | sort`
9. `find rag-security-readiness-review/02_evidence/phase_5 -maxdepth 2 -type f | sort`
10. `find rag-security-readiness-review/02_evidence/phase_3 -maxdepth 2 -type f | sort`
11. `cat AGENTS.md`
12. `sed -n '1,220p' rag-security-readiness-review/03_reports/phase_3_baseline_inventory_report.md`
13. `sed -n '1,260p' rag-security-readiness-review/03_reports/phase_5_architecture_mapping_report.md`
14. `sed -n '1,260p' rag-security-readiness-review/03_reports/phase_6_threat_model_report.md`
15. `sed -n '1,260p' rag-security-readiness-review/03_reports/phase_7_risk_taxonomy_report.md`
16. `sed -n '1,220p' rag-security-readiness-review/02_evidence/phase_3/baseline_inventory.md`
17. `sed -n '1,220p' rag-security-readiness-review/02_evidence/phase_3/important_files_index.md`
18. `sed -n '1,220p' rag-security-readiness-review/02_evidence/phase_3/security_relevant_files.md`
19. `sed -n '1,220p' rag-security-readiness-review/02_evidence/phase_5/architecture_map.md`
20. `sed -n '1,260p' rag-security-readiness-review/02_evidence/phase_6/threat_register.md`
21. `sed -n '1,260p' rag-security-readiness-review/02_evidence/phase_7/risk_taxonomy.md`
22. `for f in rag-security-readiness-review/02_evidence/phase_7/*.md; do echo '---' "$f"; sed -n '1,220p' "$f"; done`
23. `rg -n '\| [A-Z]+-[0-9]+' rag-security-readiness-review/02_evidence/phase_7/prompt_injection_risks.md rag-security-readiness-review/02_evidence/phase_7/logging_telemetry_risks.md rag-security-readiness-review/02_evidence/phase_7/auth_risks.md rag-security-readiness-review/02_evidence/phase_7/authorization_risks.md`
24. `rg -n '\| [A-Z]+-[0-9]+' rag-security-readiness-review/02_evidence/phase_7/connector_risks.md rag-security-readiness-review/02_evidence/phase_7/retrieval_acl_risks.md rag-security-readiness-review/02_evidence/phase_7/agent_risks.md`
25. `rg --files backend/onyx/auth | sort`
26. `rg --files backend/ee/onyx/auth | sort`
27. `rg --files backend/onyx/hooks | sort`
28. `rg --files web/src | rg -i 'auth|login|logout|session|token|user|password|cookie|admin|permission|role|group' | sort | head -n 200`
29. `rg --files backend/onyx/chat | sort | head -n 200`
30. `rg --files backend/onyx/document_index | sort | head -n 200`
31. `rg --files backend/onyx/connectors | sort | head -n 200`
32. `rg --files backend/onyx/server/features | sort | head -n 200`
33. `rg --files backend/onyx/tracing | sort | head -n 200`
34. `rg --files backend/onyx/server/metrics | sort | head -n 200`
35. `rg --files backend/onyx/mcp_server* backend/onyx/mcp_server | sort | head -n 200`
36. `rg --files backend/onyx/hooks | sort | head -n 200`
37. `rg --files backend/ee/onyx/external_permissions | sort | head -n 200`
38. `rg --files backend/onyx/file_processing | sort | head -n 200`
39. `rg --files . | rg '(^|/)(Dockerfile|docker-compose[^/]*\.ya?ml|pyproject\.toml|package\.json|uv\.lock|requirements[^/]*\.txt|Chart\.lock|values[^/]*\.ya?ml|devcontainer|\.env[^/]*|nginx|helm|terraform)' | sort | head -n 300`
40. `rg --files backend web deployment | rg 'Dockerfile$' | sort`
41. `rg --files deployment . | rg 'docker-compose' | sort`
42. `rg --files . | rg '(pyproject\.toml|uv\.lock|package\.json|bun\.lock|pnpm-lock\.yaml|package-lock\.json)$' | sort | head -n 200`
43. `python /tmp/phase8_gen.py`

44. `find rag-security-readiness-review/02_evidence/phase_8 -maxdepth 2 -type f | sort`
45. `find docs/security -maxdepth 1 -type f | sort`
46. `find rag-security-readiness-review/06_templates/phase_8 -maxdepth 1 -type f | sort`
47. `set -e; for d in auth authorization retrieval_acl ingestion prompt connector agent_tool_mcp logging_telemetry deployment_ci; do if [ -f "rag-security-readiness-review/02_evidence/phase_8/$d/${d}_risk_to_code.md" ]; then mv "rag-security-readiness-review/02_evidence/phase_8/$d/${d}_risk_to_code.md" "rag-security-readiness-review/02_evidence/phase_8/${d}_risk_to_code.md"; fi; done`
48. `sed -n '1,220p' rag-security-readiness-review/02_evidence/phase_8/risk_to_code_map.md`
49. `sed -n '1,220p' rag-security-readiness-review/02_evidence/phase_8/phase_8_summary.md`
50. `sed -n '1,220p' rag-security-readiness-review/02_evidence/commands/phase_8_risk_to_code_commands_executed.md`
51. `sed -n '1,8p' docs/security/risk_to_code_map.md`
52. `sed -n '1,80p' rag-security-readiness-review/02_evidence/phase_8/risk_to_code_limitations.md`
53. `python - <<'PY' ...fix duplicate limitations heading... PY`
54. `sed -n '1,20p' rag-security-readiness-review/02_evidence/phase_8/risk_to_code_limitations.md`
55. `sed -n '1,8p' docs/security/risk_to_code_limitations.md`
56. `git status --short`
57. `for f in risk_to_code_map.md auth_risk_to_code.md authorization_risk_to_code.md retrieval_acl_risk_to_code.md ingestion_risk_to_code.md prompt_risk_to_code.md connector_risk_to_code.md agent_tool_mcp_risk_to_code.md logging_telemetry_risk_to_code.md deployment_ci_risk_to_code.md control_candidate_register.md missing_control_candidates.md unverified_mappings.md risk_to_code_limitations.md phase_8_summary.md; do test -f "rag-security-readiness-review/02_evidence/phase_8/$f" && echo "OK $f" || echo "MISSING $f"; done`
58. `for f in phase_3_inventory_sources_reviewed.txt phase_5_architecture_sources_reviewed.txt phase_6_threat_sources_reviewed.txt phase_7_risk_sources_reviewed.txt auth_code_search_raw.txt authorization_code_search_raw.txt retrieval_acl_code_search_raw.txt ingestion_code_search_raw.txt prompt_code_search_raw.txt connector_code_search_raw.txt agent_tool_mcp_code_search_raw.txt logging_telemetry_code_search_raw.txt deployment_ci_code_search_raw.txt risk_to_code_map_raw.txt; do test -f "rag-security-readiness-review/02_evidence/phase_8/raw_outputs/$f" && echo "OK $f" || echo "MISSING $f"; done`
59. `for f in risk_to_code_map.md auth_risk_to_code.md authorization_risk_to_code.md retrieval_acl_risk_to_code.md ingestion_risk_to_code.md prompt_risk_to_code.md connector_risk_to_code.md agent_tool_mcp_risk_to_code.md logging_telemetry_risk_to_code.md deployment_ci_risk_to_code.md phase_8_risk_to_code_index.md; do test -f "docs/security/$f" && echo "OK $f" || echo "MISSING $f"; done`
60. `for f in docs/security/risk_to_code_map.md docs/security/auth_risk_to_code.md docs/security/authorization_risk_to_code.md docs/security/retrieval_acl_risk_to_code.md docs/security/ingestion_risk_to_code.md docs/security/prompt_risk_to_code.md docs/security/connector_risk_to_code.md docs/security/agent_tool_mcp_risk_to_code.md docs/security/logging_telemetry_risk_to_code.md docs/security/deployment_ci_risk_to_code.md docs/security/phase_8_risk_to_code_index.md; do first=$(head -n 1 "$f"); case "$first" in "> This is the client-facing mirror"*) echo "OK $f";; *) echo "BAD $f :: $first";; esac; done`
61. `rg -n "\bVALIDATED\b" rag-security-readiness-review/02_evidence/phase_8 rag-security-readiness-review/03_reports/phase_8_risk_to_code_mapping_report.md docs/security/risk_to_code_map.md docs/security/*_risk_to_code.md || true`
62. `cat rag-security-readiness-review/02_evidence/phase_8/phase_8_generated_counts.txt`
63. `git status --short`
64. `python - <<'PY' ...synchronize missing-candidate counts across PHASE 8 summary, map, report, raw summary... PY`
65. `sed -n '25,60p' rag-security-readiness-review/02_evidence/phase_8/phase_8_summary.md`
66. `rg -n "Missing control candidate summary|missing control candidates" rag-security-readiness-review/03_reports/phase_8_risk_to_code_mapping_report.md`
67. `cat rag-security-readiness-review/02_evidence/phase_8/phase_8_generated_counts.txt`
68. `git diff --check`
69. `git status --short | sed -n '1,200p'`
70. `test -f rag-security-readiness-review/03_reports/phase_8_risk_to_code_mapping_report.md && echo OK || echo MISSING`
71. `git add rag-security-readiness-review/02_evidence/phase_8 rag-security-readiness-review/02_evidence/commands/phase_8_risk_to_code_commands_executed.md rag-security-readiness-review/03_reports/phase_8_risk_to_code_mapping_report.md rag-security-readiness-review/06_templates/phase_8 docs/security`
72. `git status --short`
