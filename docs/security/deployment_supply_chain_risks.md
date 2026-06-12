> This is the client-facing mirror of the PHASE 7 evidence file. The canonical evidence copy remains under rag-security-readiness-review/02_evidence/phase_7/.

# Deployment/Supply-Chain Risks

## Category purpose

Capture repository-backed deployment and build-path risks that may expose secrets or runtime misconfiguration.

## Scope

Deployment manifests, Docker/runtime configuration, CI/CD references, and supply-chain posture.

## Related PHASE 5 architecture evidence

- rag-security-readiness-review/02_evidence/phase_5/deployment_flow_map.md
- rag-security-readiness-review/02_evidence/phase_5/architecture_map.md

## Related PHASE 6 threats

- TH-12
- TH-15
- TH-16

## Protected assets affected

Deployment secrets; runtime configuration; build artifacts; container settings

## Actors involved

Deployment/operator role; CI/CD actor; malicious insider

## Trust boundaries involved

Deployment/runtime; CI/CD and supply-chain; container/runtime

## Data flows involved

Repository configuration into deployment artifacts; build artifacts into runtime; secret handling across deployment stages

## Risk list

| Risk ID | Risk | Evidence label | Related PHASE 6 threat ID | Related PHASE 5 evidence | Affected assets | Actors | Trust boundaries | Potential impact | Missing evidence | Later validation method | Priority |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| DEP-01 | Exposed deployment secrets can weaken the runtime and adjacent systems. | EVIDENCE-LINKED | TH-15 | deployment_flow_map.md; architecture_map.md | Deployment secrets; runtime configuration; build artifacts; container settings | Deployment/operator role; CI/CD actor; malicious insider | Deployment/runtime; CI/CD and supply-chain; container/runtime | Secrets or service endpoints may be exposed to broader access. | No live deployment inspection. | Later deployment hardening review. | Critical candidate |
| DEP-02 | Insecure environment configuration can expose services or weaken access controls. | EVIDENCE-LINKED | TH-15 | deployment_flow_map.md; architecture_map.md | Deployment secrets; runtime configuration; build artifacts; container settings | Deployment/operator role; CI/CD actor; malicious insider | Deployment/runtime; CI/CD and supply-chain; container/runtime | Services may be overexposed or under-protected. | No live environment review. | Later environment-config review. | High candidate |
| DEP-03 | Unverified production deployment target leaves the real target environment unknown. | UNVERIFIED | TH-15 | deployment_flow_map.md; architecture_map.md | Deployment secrets; runtime configuration; build artifacts; container settings | Deployment/operator role; CI/CD actor; malicious insider | Deployment/runtime; CI/CD and supply-chain; container/runtime | The review cannot confirm where the repository actually deploys. | No deployed-target evidence. | Later deployed-target review. | Informational |
| DEP-04 | CI/CD secret leakage remains unverified when workflow evidence is absent. | UNVERIFIED | TH-16 | deployment_flow_map.md; architecture_map.md | Deployment secrets; runtime configuration; build artifacts; container settings | Deployment/operator role; CI/CD actor; malicious insider | Deployment/runtime; CI/CD and supply-chain; container/runtime | Secrets or artifacts could be exposed if workflows exist outside the reviewed source set. | No CI workflow evidence identified. | Later supply-chain inventory if workflows appear. | Medium candidate |
| DEP-05 | Dependency or supply-chain compromise can alter artifacts before deployment. | UNVERIFIED | TH-16 | deployment_flow_map.md; architecture_map.md | Deployment secrets; runtime configuration; build artifacts; container settings | Deployment/operator role; CI/CD actor; malicious insider | Deployment/runtime; CI/CD and supply-chain; container/runtime | Artifact integrity may be reduced before runtime delivery. | No dependency or workflow validation. | Later supply-chain inventory review. | Medium candidate |
| DEP-06 | Container or runtime misconfiguration can expose internal services or secrets. | INFERRED | TH-15, TH-12 | deployment_flow_map.md; architecture_map.md | Deployment secrets; runtime configuration; build artifacts; container settings | Deployment/operator role; CI/CD actor; malicious insider | Deployment/runtime; CI/CD and supply-chain; container/runtime | Runtime isolation may be weaker than intended. | No live container/runtime review. | Later container-runtime review. | High candidate |

## Missing evidence

No live deployment inspection; no CI workflow evidence review beyond repository search; no runtime secret audit.

## Later validation methods

Deployment hardening review; CI/CD inventory review if workflows are added; runtime secret and configuration validation.

## Non-claims

No claim that production deployment is safe; no claim that supply-chain paths are verified; no claim that deployed configuration is known.

## Client-ready summary

The category records the deployment and supply-chain surface while preserving the limitation that no live environment was inspected.
