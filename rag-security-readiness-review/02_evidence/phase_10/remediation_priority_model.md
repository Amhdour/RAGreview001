# PHASE 10 Remediation Priority Model

## Purpose
This model assigns candidate remediation priority to PHASE 10 control gaps without claiming final severity, exploitability, or production readiness.

## Priority labels
- P0 candidate: likely launch-blocking if validated.
- P1 candidate: should be fixed before production use or wider rollout if validated.
- P2 candidate: important hardening or evidence gap.
- P3 candidate: documentation, monitoring, or low-risk improvement.
- Unverified: needs more evidence before prioritization.

## How priority is assigned
Priority is based on the control category, related PHASE 7 risk, related PHASE 6 threat, PHASE 8 control candidate status, PHASE 9 evidence/test status, PHASE 10A authorization finding where applicable, and missing evidence.

## How priority must not be interpreted
- Priority is not a claim that a vulnerability exists.
- Priority is not a claim of exploitability.
- Priority is not a production readiness decision.
- Priority is not a test result or CI result.
- Priority does not convert candidate severity into final severity.

## Examples of candidate logic
- P0 candidate: retrieval ACL runtime validation is missing for search-time access control and would likely be launch-blocking if the gap is validated.
- P1 candidate: authorization deny/allow coverage, connector credential lifecycle evidence, telemetry redaction proof, and CI workflow evidence should be addressed before production use or wider rollout if validated.
- P2 candidate: governance documentation, limitation tracking, and evidence traceability are important hardening and evidence gaps.
- P3 candidate: low-risk documentation cleanup or index consolidation can be assigned when technical control impact is limited.
- Unverified: original-source/working-copy and production evidence gaps need more evidence before technical prioritization.

## Relationship to later validation
Later phases should replace candidate priority with evidence-backed prioritization only after approved runtime tests, CI evidence, production-like review, or owner attestation is available.
