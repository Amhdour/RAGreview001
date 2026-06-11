> This is the client-facing mirror of the PHASE 2 evidence file. The canonical evidence copy remains under rag-security-readiness-review/02_evidence/phase_2/.

# Phase 2 Severity Scale

## Critical
- Meaning: Immediate security risk that can enable serious compromise, unauthorized access, or major data exposure.
- RAG/agent example: A tool-call path allows arbitrary file access outside the intended sandbox.
- Evidence required: Direct source evidence, reproduction evidence when safe, and impact analysis.
- Remediation urgency: Immediate.

## High
- Meaning: Severe risk with meaningful potential for privilege escalation, data leakage, or unsafe tool execution.
- RAG/agent example: Retrieval or agent tooling can bypass access checks for restricted documents.
- Evidence required: Source evidence, control review, and validation of the affected path where feasible.
- Remediation urgency: Very high.

## Medium
- Meaning: Material weakness that could contribute to abuse or reduced security assurance.
- RAG/agent example: Logging may expose more metadata than necessary but not full secrets.
- Evidence required: Source review and contextual assessment.
- Remediation urgency: Planned remediation recommended.

## Low
- Meaning: Limited security concern or defense-in-depth gap with modest impact.
- RAG/agent example: A security-related configuration default is present but constrained by other controls.
- Evidence required: Source review and control comparison.
- Remediation urgency: Backlog or scheduled improvement.

## Informational
- Meaning: Observation, hardening note, or documentation gap without direct security impact.
- RAG/agent example: A security-related setting is documented inconsistently across files.
- Evidence required: Source review and documentation comparison.
- Remediation urgency: Optional or opportunistic.

## Unverified
- Meaning: A potential issue was noted, but evidence is insufficient to classify it confidently.
- RAG/agent example: A suspicious config path exists, but runtime effect is unknown.
- Evidence required: More evidence from later phases.
- Remediation urgency: Investigate before assigning final severity.
