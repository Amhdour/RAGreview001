> This is the client-facing mirror of the PHASE 2 evidence file. The canonical evidence copy remains under rag-security-readiness-review/02_evidence/phase_2/.

# Phase 2 Testing Rules

## Allowed actions
- Static source inspection
- File inventory
- Dependency file review
- Config review
- Documentation review
- Test plan creation
- Synthetic local test design
- Safe non-destructive local checks
- Secret-pattern scanning if authorized and local
- No real secrets
- No real customer data

## Forbidden actions
- Production testing
- Destructive testing
- DoS testing
- Unauthorized scanning
- Credential attacks
- Real phishing/social engineering
- Malware execution
- Exfiltration testing
- Testing against third-party systems without permission
- Modifying original source snapshot
- Claiming production readiness without evidence

## Safe execution expectations
- Prefer read-only checks.
- Keep all checks local and non-destructive.
- Do not interact with production or live customer environments.
- Do not run exploit payloads or adversarial validation in this phase.

## Reporting rule
Any proposed test that would require live systems, real credentials, destructive actions, or unauthorized access must be deferred and explicitly labeled as out of scope.
