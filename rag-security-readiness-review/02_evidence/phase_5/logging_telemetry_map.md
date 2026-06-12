# PHASE 5 Logging / Telemetry Map

## 1. Purpose
This map identifies repository evidence for backend logging, telemetry, memory logging, metrics, tracing, and frontend instrumentation.

## 2. Scope
- In scope: `backend/onyx/utils/logger.py`, `backend/onyx/utils/telemetry.py`, `backend/onyx/utils/memory_logger.py`, `backend/onyx/server/metrics/`, `backend/onyx/tracing/`, `backend/onyx/main.py`, `web/src/instrumentation.ts`, and `web/src/instrumentation-client.ts`.
- Out of scope: live observability dashboards, production log retention, production alerting rules, and telemetry destinations not represented by repository files.

## 3. Main entry points
- Backend logger setup: `backend/onyx/utils/logger.py`.
- Backend telemetry helper: `backend/onyx/utils/telemetry.py`.
- Memory logger: `backend/onyx/utils/memory_logger.py`.
- Metrics package: `backend/onyx/server/metrics/`.
- Prometheus setup: `backend/onyx/server/metrics/prometheus_setup.py`.
- Metrics server/auth: `backend/onyx/server/metrics/metrics_server.py`, `backend/onyx/server/metrics/metrics_auth.py`.
- Request/latency metrics: `backend/onyx/server/metrics/slow_requests.py`, `backend/onyx/server/middleware/latency_logging.py`.
- Tracing setup and flow registry: `backend/onyx/tracing/setup.py`, `backend/onyx/tracing/flows.py`, `backend/onyx/tracing/llm_utils.py`.
- Backend app startup instrumentation: `backend/onyx/main.py`.
- Frontend instrumentation: `web/src/instrumentation.ts`, `web/src/instrumentation-client.ts`.

## 4. Architecture flow
1. Backend modules call `setup_logger()` from `backend/onyx/utils/logger.py` for logging.
2. `backend/onyx/utils/telemetry.py` provides telemetry helper functions used by backend code.
3. `backend/onyx/main.py` initializes tracing and registers metrics-related startup behavior.
4. Metrics-specific files under `backend/onyx/server/metrics/` define Prometheus setup, metrics endpoint/auth support, and domain metrics for Celery, connectors, deletion, embedding, indexing, image processing, per-tenant state, permissions sync, Postgres pools, pruning, and slow requests.
5. LLM/tracing files under `backend/onyx/tracing/` define tracing setup, flow values, and LLM tracing utilities.
6. Frontend instrumentation is split between `web/src/instrumentation.ts` and `web/src/instrumentation-client.ts`.

## 5. Supporting evidence
- `backend/onyx/utils/logger.py` — backend logger setup.
- `backend/onyx/utils/telemetry.py` — telemetry helpers and record types.
- `backend/onyx/utils/memory_logger.py` — memory logging helper.
- `backend/onyx/server/metrics/prometheus_setup.py` — Prometheus metrics setup.
- `backend/onyx/server/metrics/metrics_server.py`, `backend/onyx/server/metrics/metrics_auth.py` — metrics server/auth files.
- `backend/onyx/server/metrics/celery_task_metrics.py`, `backend/onyx/server/metrics/connector_health_metrics.py`, `backend/onyx/server/metrics/indexing_pipeline.py`, `backend/onyx/server/metrics/postgres_connection_pool.py`, `backend/onyx/server/metrics/slow_requests.py` — domain metric files.
- `backend/onyx/tracing/setup.py`, `backend/onyx/tracing/flows.py`, `backend/onyx/tracing/llm_utils.py` — tracing setup, flow registry, and LLM tracing utilities.
- `backend/onyx/main.py` — app-level tracing and metrics initialization imports/calls.
- `web/src/instrumentation.ts`, `web/src/instrumentation-client.ts` — frontend instrumentation files.

## 6. Dependencies
- Internal dependencies: backend app startup and feature modules depend on logger, telemetry, metrics, and tracing utilities.
- External services/infrastructure supported by files: Sentry imports/config in `backend/onyx/main.py`; Prometheus-related setup in `backend/onyx/server/metrics/prometheus_setup.py`; tracing processors under `backend/onyx/tracing/`.

## 7. Gaps / unknowns
- Actual production telemetry destinations, retention periods, dashboards, and alert policies are not established by source files.
- Whether telemetry is enabled at runtime depends on deployment configuration and credentials.

## 8. Client-ready summary
The repository includes backend logging, telemetry helpers, Prometheus metrics modules, tracing utilities, and frontend instrumentation files. These files show where observability is implemented, but they do not prove which telemetry systems are enabled in a live deployment.

## Support table
| Claim | Evidence file paths | Support status | Notes |
|---|---|---:|---|
| Backend logger setup is centralized in a utility file. | `backend/onyx/utils/logger.py` | Supported | Logger utility file exists. |
| Backend telemetry helper code exists. | `backend/onyx/utils/telemetry.py` | Supported | Telemetry utility file exists. |
| Memory logging helper code exists. | `backend/onyx/utils/memory_logger.py` | Supported | Memory logger file exists. |
| Backend metrics are grouped under a metrics server package. | `backend/onyx/server/metrics/` | Supported | The directory contains Prometheus and domain metrics files. |
| LLM/tracing flow registry and setup code exist. | `backend/onyx/tracing/setup.py`, `backend/onyx/tracing/flows.py`, `backend/onyx/tracing/llm_utils.py` | Supported | Tracing files exist. |
| Frontend instrumentation files exist. | `web/src/instrumentation.ts`, `web/src/instrumentation-client.ts` | Supported | Server/client instrumentation files exist. |
| Live telemetry retention and alert policies are known. | No repository evidence identified. | Unsupported | Operational policy is not in reviewed source files. |

## Missing or unsupported items
- Runtime telemetry enablement, retention, dashboard configuration, and alerting policies are unsupported by repository files alone.
