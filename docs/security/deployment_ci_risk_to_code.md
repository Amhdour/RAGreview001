> This is the client-facing mirror of the PHASE 8 evidence file. The canonical evidence copy remains under rag-security-readiness-review/02_evidence/phase_8/.

# Deployment/CI Risk to Code

## Category purpose
Map Dockerfiles, compose files, Helm/Kubernetes manifests, Terraform, package manifests, and CI references that can shape runtime and build-time security.

## Related PHASE 7 risks
- DEP-01
- DEP-02
- DEP-03
- DEP-04
- DEP-05
- DEP-06

## Related PHASE 6 threats
- TH-12
- TH-15
- TH-16

## Related PHASE 5 architecture evidence
- rag-security-readiness-review/02_evidence/phase_5/deployment_flow_map.md
- rag-security-readiness-review/02_evidence/phase_5/architecture_map.md

## Related PHASE 3 inventory evidence
- rag-security-readiness-review/02_evidence/phase_3/baseline_inventory.md
- rag-security-readiness-review/02_evidence/phase_3/important_files_index.md
- rag-security-readiness-review/02_evidence/phase_3/security_relevant_files.md

## Candidate Onyx file paths
- backend/Dockerfile
- web/Dockerfile
- deployment/docker_compose/docker-compose.yml
- deployment/helm/charts/onyx/templates/configmap.yaml
- deployment/helm/charts/onyx/templates/auth-secrets.yaml
- deployment/data/nginx/app.conf.template
- deployment/terraform/modules/aws/onyx/main.tf
- pyproject.toml
- backend/uv.lock
- web/package.json
- uv.lock
- .github/workflows/*

## Existing control candidates
- DEP-MAP-01: Docker and compose runtime paths appear present.
- DEP-MAP-02: Helm, nginx, secrets, and Terraform paths appear present.

## Missing control candidates
- No `.github/workflows` path was found in the current checkout.

## Unverified mappings
- Deployment hardening remains source-only and untested.

## Later validation methods
- Container hardening review.
- Helm/nginx/Terraform runtime review.
- CI/workflow inventory if workflows appear later.

## Non-claims
- No claim that deployment is safe.
- No claim that CI workflows exist or are secure.

## Client-ready summary
Deployment and CI evidence comes from Docker, Helm, runtime config, and package files, while the workflow directory itself was not present in this checkout.

## Mapping table

| Mapping ID | Related risk ID/category | Related PHASE 6 threat ID | Related PHASE 5 architecture evidence | Candidate Onyx file/path | Mapping label | Why this file/path matters | Missing evidence | Later validation method | Notes |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| DEP-MAP-01 | DEP-01 / DEP-02 | TH-15 | deployment_flow_map.md; architecture_map.md | backend/Dockerfile; web/Dockerfile; deployment/docker_compose/docker-compose.yml | EXISTING-CANDIDATE | These build and compose files appear to control the containerized runtime shape and service exposure. | No live deployment inspection or runtime hardening validation was performed. | Container and compose hardening review. | Source-backed deployment candidate only. |
| DEP-MAP-02 | DEP-02 / DEP-06 | TH-12 / TH-15 | deployment_flow_map.md; architecture_map.md | deployment/helm/charts/onyx/templates/configmap.yaml; deployment/helm/charts/onyx/templates/auth-secrets.yaml; deployment/data/nginx/app.conf.template; deployment/terraform/modules/aws/onyx/main.tf | EXISTING-CANDIDATE | These manifests and runtime templates appear to control environment configuration, secrets wiring, and network exposure. | No runtime or deployed-target validation was collected. | Helm, nginx, and Terraform runtime review. | Candidate path for deployment hardening. |
| DEP-MAP-03 | DEP-03 / DEP-04 / DEP-05 | TH-16 | deployment_flow_map.md; architecture_map.md | NOT FOUND — .github/workflows/* (no .github directory existed in this checkout); pyproject.toml; backend/uv.lock; web/package.json | MISSING-CANDIDATE | The repository search did not identify a GitHub Actions workflow directory, so CI-specific hardening evidence was not available in source. | No `.github/workflows` evidence exists in the current checkout for this pass. | CI/workflow inventory if workflows are added later. | This is the clearest deployment/CI evidence gap in the current source tree. |
