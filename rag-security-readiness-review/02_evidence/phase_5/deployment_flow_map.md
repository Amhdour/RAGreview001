# PHASE 5 Deployment Flow Map

## 1. Purpose
This map identifies repository evidence for deployment packaging, compose/Helm/cloud deployment files, nginx routing templates, runtime entry points, and build sandbox deployment support.

## 2. Scope
- In scope: `deployment/`, docker-compose files under `deployment/docker_compose/`, `backend/Dockerfile`, `backend/Dockerfile.model_server`, `web/Dockerfile`, `backend/onyx/server/features/build/sandbox/`, `backend/onyx/server/runtime/`, and runtime entry point files identified in the repository.
- Out of scope: actual deployed infrastructure, secrets, production environment variables, cloud account resources, and runtime health not represented by repository files.

## 3. Main entry points
- Deployment root: `deployment/README.md`.
- Docker Compose deployment files: `deployment/docker_compose/docker-compose.yml`, `deployment/docker_compose/docker-compose.prod.yml`, `deployment/docker_compose/docker-compose.prod-no-letsencrypt.yml`, `deployment/docker_compose/docker-compose.dev.yml`, `deployment/docker_compose/docker-compose.onyx-lite.yml`, `deployment/docker_compose/docker-compose.craft.yml`, and peer compose files under `deployment/docker_compose/`.
- Compose environment templates: `deployment/docker_compose/env.template`, `deployment/docker_compose/env.prod.template`, `deployment/docker_compose/env.nginx.template`.
- Dockerfiles: `backend/Dockerfile`, `backend/Dockerfile.model_server`, `web/Dockerfile`, `.devcontainer/Dockerfile`.
- Nginx templates/scripts: `deployment/data/nginx/app.conf.template`, `deployment/data/nginx/app.conf.template.prod`, `deployment/data/nginx/app.conf.template.no-letsencrypt`, `deployment/data/nginx/mcp.conf.inc.template`, `deployment/data/nginx/mcp_upstream.conf.inc.template`, `deployment/data/nginx/run-nginx.sh`.
- Helm/Kubernetes files: `deployment/helm/`, `backend/onyx/server/features/build/sandbox/kubernetes/`.
- AWS ECS Fargate files: `deployment/aws_ecs_fargate/cloudformation/`.
- Build sandbox files: `backend/onyx/server/features/build/sandbox/`, including `backend/onyx/server/features/build/sandbox/image/Dockerfile`, `backend/onyx/server/features/build/sandbox/docker/docker_sandbox_manager.py`, `backend/onyx/server/features/build/sandbox/kubernetes/kubernetes_sandbox_manager.py`, and `backend/onyx/server/features/build/sandbox/base.py`.
- Runtime package: `backend/onyx/server/runtime/` if present in this repository checkout.

## 4. Architecture flow
1. Application containers are represented by Dockerfiles for backend, model server, and web frontend.
2. Local/self-hosted deployment wiring is represented by Docker Compose files and compose environment templates under `deployment/docker_compose/`.
3. HTTP/nginx routing templates are represented under `deployment/data/nginx/`, including MCP-specific nginx include templates.
4. Kubernetes/Helm deployment support is represented by `deployment/helm/` and build sandbox Kubernetes manager files.
5. AWS ECS Fargate deployment support is represented by CloudFormation files under `deployment/aws_ecs_fargate/cloudformation/`.
6. The build/craft sandbox has its own Docker image files, entrypoint scripts, sandbox daemon files, Docker manager, Kubernetes manager, SSE/transport helpers, and task files under `backend/onyx/server/features/build/sandbox/`.

## 5. Supporting evidence
- `deployment/README.md` — deployment documentation entry point.
- `deployment/docker_compose/` — Docker Compose files and environment templates.
- `backend/Dockerfile`, `backend/Dockerfile.model_server`, `web/Dockerfile` — container build files.
- `deployment/data/nginx/app.conf.template`, `deployment/data/nginx/mcp.conf.inc.template`, `deployment/data/nginx/mcp_upstream.conf.inc.template`, `deployment/data/nginx/run-nginx.sh` — nginx routing templates/scripts.
- `deployment/helm/` — Helm deployment files.
- `deployment/aws_ecs_fargate/cloudformation/` — AWS CloudFormation deployment files.
- `backend/onyx/server/features/build/sandbox/README.md`, `backend/onyx/server/features/build/sandbox/image/Dockerfile`, `backend/onyx/server/features/build/sandbox/image/entrypoint.sh`, `backend/onyx/server/features/build/sandbox/image/sidecar-entrypoint.sh` — sandbox deployment/image evidence.
- `backend/onyx/server/features/build/sandbox/docker/docker_sandbox_manager.py`, `backend/onyx/server/features/build/sandbox/kubernetes/kubernetes_sandbox_manager.py` — sandbox runtime manager evidence.

## 6. Dependencies
- Internal dependencies: deployment files package the backend, web frontend, model server, nginx, and sandbox-related components.
- External services/infrastructure supported by files: Docker/Docker Compose, nginx, Helm/Kubernetes, AWS ECS Fargate/CloudFormation, and sandbox container/Kubernetes managers.

## 7. Gaps / unknowns
- Actual production topology, secrets, live environment variables, replica counts, and cloud resources are not known from repository files alone.
- The presence of multiple compose files does not prove which one is used in production.
- `backend/onyx/server/runtime/` was included in scope by mission requirements; if absent in a checkout, runtime claims for that path should be treated as unsupported.

## 8. Client-ready summary
Deployment evidence shows the project can be packaged into backend, frontend, and model-server containers, with Docker Compose, Helm/Kubernetes, nginx, and AWS ECS Fargate materials present in the repository. The craft/build sandbox has separate image, entrypoint, Docker manager, and Kubernetes manager files. The repository does not prove the exact live production deployment.

## Support table
| Claim | Evidence file paths | Support status | Notes |
|---|---|---:|---|
| Backend, model server, and frontend container build files exist. | `backend/Dockerfile`, `backend/Dockerfile.model_server`, `web/Dockerfile` | Supported | Dockerfiles are present. |
| Docker Compose deployment wiring exists. | `deployment/docker_compose/docker-compose.yml`, `deployment/docker_compose/docker-compose.prod.yml`, `deployment/docker_compose/env.template` | Supported | Compose files and environment templates are present. |
| Nginx routing templates exist, including MCP-specific templates. | `deployment/data/nginx/app.conf.template`, `deployment/data/nginx/mcp.conf.inc.template`, `deployment/data/nginx/mcp_upstream.conf.inc.template` | Supported | Nginx templates are present. |
| Helm/Kubernetes deployment support exists. | `deployment/helm/`, `backend/onyx/server/features/build/sandbox/kubernetes/kubernetes_sandbox_manager.py` | Supported | Helm directory and sandbox Kubernetes manager exist. |
| AWS ECS Fargate deployment support exists. | `deployment/aws_ecs_fargate/cloudformation/` | Supported | CloudFormation deployment files are present. |
| Build sandbox has dedicated deployment/runtime files. | `backend/onyx/server/features/build/sandbox/image/Dockerfile`, `backend/onyx/server/features/build/sandbox/docker/docker_sandbox_manager.py`, `backend/onyx/server/features/build/sandbox/kubernetes/kubernetes_sandbox_manager.py` | Supported | Sandbox image and manager files are present. |
| Exact production deployment topology is known. | No repository evidence identified. | Unsupported | Runtime deployment depends on external environment and selected manifests. |
| Runtime package architecture under `backend/onyx/server/runtime/` is known. | `backend/onyx/server/runtime/` not confirmed in this checkout. | Unsupported | Mission requested this path, but no claim is made unless path exists. |

## Missing or unsupported items
- Exact production topology, selected deployment manifest, secrets, live environment variables, replica counts, and cloud resources are unsupported by repository files alone.
- `backend/onyx/server/runtime/` architecture is unsupported if that path is absent in this repository checkout.
