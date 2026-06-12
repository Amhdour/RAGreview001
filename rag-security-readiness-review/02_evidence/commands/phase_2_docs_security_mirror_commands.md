# PHASE 2 Docs Security Mirror Commands

## Commands executed

~~~bash
pwd && find .. -name AGENTS.md -print
~~~

~~~bash
git status --short && find rag-security-readiness-review/02_evidence/phase_2 -maxdepth 1 -type f -printf '%f\n' | sort && find rag-security-readiness-review/02_evidence/commands -maxdepth 1 -type f -printf '%f\n' | sort
~~~

~~~bash
for f in scope.md claim_boundaries.md access_level_limitations.md assumptions.md constraints.md testing_rules.md evidence_standard.md severity_scale.md readiness_scoring_scale.md go_no_go_criteria.md; do echo '---' $f; sed -n '1,80p' rag-security-readiness-review/02_evidence/phase_2/$f; done
~~~

~~~bash
python - <<'PY'
from pathlib import Path
src_dir = Path('rag-security-readiness-review/02_evidence/phase_2')
dst_dir = Path('docs/security')
dst_dir.mkdir(parents=True, exist_ok=True)
files = [
    'scope.md',
    'claim_boundaries.md',
    'access_level_limitations.md',
    'assumptions.md',
    'constraints.md',
    'testing_rules.md',
    'evidence_standard.md',
    'severity_scale.md',
    'readiness_scoring_scale.md',
    'go_no_go_criteria.md',
]
header = (
    '> This is the client-facing mirror of the PHASE 2 evidence file. The canonical evidence copy remains under '
    'rag-security-readiness-review/02_evidence/phase_2/.\n\n'
)
purposes = {
    'scope.md': 'Defines the PHASE 2 review scope, objectives, included and excluded components, and review activities.',
    'claim_boundaries.md': 'Defines confirmed, conditional, unsupported, forbidden, and client-safe claims for PHASE 2.',
    'access_level_limitations.md': 'Documents source-only access limits and what cannot be proven without live or production access.',
    'assumptions.md': 'Records assumptions that constrain PHASE 2 conclusions until later evidence confirms or refutes them.',
    'constraints.md': 'Documents operational, safety, evidence, and claim constraints for PHASE 2 work.',
    'testing_rules.md': 'Defines safe testing boundaries and prohibited activities for current and later validation work.',
    'evidence_standard.md': 'Defines the evidence quality, command recording, redaction, and source reference standards.',
    'severity_scale.md': 'Defines severity levels and evidence expectations for future security findings.',
    'readiness_scoring_scale.md': 'Defines readiness levels, review categories, and scoring interpretation rules.',
    'go_no_go_criteria.md': 'Defines future GO, GO WITH CONDITIONS, NO-GO, and UNVERIFIED decision criteria.',
}
for name in files:
    content = (src_dir / name).read_text()
    (dst_dir / name).write_text(header + content)

lines = [
    '# PHASE 2 Docs Security Mirror Index',
    '',
    '## PHASE 2 status',
    'COMPLETE WITH LIMITATIONS',
    '',
    '## Next phase',
    'PHASE 3 — Create baseline inventory',
    '',
    '## Mirrored files',
    '',
    '| Mirrored file | Canonical evidence source path | Purpose |',
    '| --- | --- | --- |',
]
for name in files:
    lines.append(
        f'| `docs/security/{name}` | `rag-security-readiness-review/02_evidence/phase_2/{name}` | {purposes[name]} |'
    )
lines.extend([
    '',
    '## Mirror note',
    'Each mirrored file includes a header stating that it is the client-facing mirror and that the canonical evidence copy remains under `rag-security-readiness-review/02_evidence/phase_2/`.',
    '',
])
(dst_dir / 'phase_2_index.md').write_text('\n'.join(lines))
PY
~~~

~~~bash
cat > rag-security-readiness-review/02_evidence/commands/phase_2_docs_security_mirror_commands.md <<'EOF'
# PHASE 2 Docs Security Mirror Commands
...
EOF
~~~

Result: this combined shell command failed after creating the mirror files because of a shell quoting issue while recording the command log (`unexpected EOF while looking for matching \`\``). The command log was rewritten after the failure.

~~~bash
git status --short && find docs/security -maxdepth 1 -type f -printf '%f\n' 2>/dev/null | sort && [ -f rag-security-readiness-review/02_evidence/commands/phase_2_docs_security_mirror_commands.md ] && sed -n '1,60p' rag-security-readiness-review/02_evidence/commands/phase_2_docs_security_mirror_commands.md || true
~~~

~~~bash
cat > rag-security-readiness-review/02_evidence/commands/phase_2_docs_security_mirror_commands.md <<'EOF'
# PHASE 2 Docs Security Mirror Commands
...
EOF
~~~

~~~bash
for f in docs/security/*.md; do echo '---' $f; sed -n '1,5p' "$f"; done
printf '\nIndex:\n'; sed -n '1,80p' docs/security/phase_2_index.md
printf '\nDiff stats/status:\n'; git status --short
~~~

~~~bash
python - <<'PY'
from pathlib import Path
src_dir = Path('rag-security-readiness-review/02_evidence/phase_2')
dst_dir = Path('docs/security')
files = [
    'scope.md',
    'claim_boundaries.md',
    'access_level_limitations.md',
    'assumptions.md',
    'constraints.md',
    'testing_rules.md',
    'evidence_standard.md',
    'severity_scale.md',
    'readiness_scoring_scale.md',
    'go_no_go_criteria.md',
]
header = (
    '> This is the client-facing mirror of the PHASE 2 evidence file. The canonical evidence copy remains under '
    'rag-security-readiness-review/02_evidence/phase_2/.\n\n'
)
for name in files:
    mirrored = (dst_dir / name).read_text()
    assert mirrored.startswith(header), name
    assert mirrored[len(header):] == (src_dir / name).read_text(), name
print(f'Verified {len(files)} mirrored files with required header and matching canonical content.')
PY
~~~
