# Logging/Telemetry Risk to Code

## Category purpose
Map logging, tracing, metrics, redaction, and observability code that may capture prompts, documents, tokens, or other sensitive data.

## Related PHASE 7 risks
- LOG-01
- LOG-02
- LOG-03
- LOG-04
- LOG-05
- PI-05

## Related PHASE 6 threats
- TH-10
- TH-13
- TH-15

## Related PHASE 5 architecture evidence
- rag-security-readiness-review/02_evidence/phase_5/logging_telemetry_map.md
- rag-security-readiness-review/02_evidence/phase_5/backend_architecture.md
- rag-security-readiness-review/02_evidence/phase_5/deployment_flow_map.md

## Related PHASE 3 inventory evidence
- rag-security-readiness-review/02_evidence/phase_3/baseline_inventory.md
- rag-security-readiness-review/02_evidence/phase_3/important_files_index.md
- rag-security-readiness-review/02_evidence/phase_3/security_relevant_files.md

## Candidate Onyx file paths
- backend/onyx/tracing/flows.py
- backend/onyx/tracing/llm_utils.py
- backend/onyx/tracing/setup.py
- backend/onyx/tracing/masking.py
- backend/onyx/tracing/framework/spans.py
- backend/onyx/tracing/framework/traces.py
- backend/onyx/tracing/langfuse_tracing_processor.py
- backend/ee/onyx/utils/telemetry.py
- backend/onyx/server/metrics/metrics_server.py
- backend/onyx/server/metrics/metrics_auth.py
- backend/onyx/server/metrics/prometheus_setup.py

## Existing control candidates
- LOG-MAP-01: tracing setup and flow files appear present.
- LOG-MAP-02: masking, spans, traces, telemetry, and metrics files appear present.

## Missing control candidates
- No dedicated end-to-end redaction proof was identified.

## Unverified mappings
- Logging and telemetry redaction remains source-only and unverified.

## Later validation methods
- Log-redaction review.
- Telemetry sink review.
- Sensitive-field filtering validation.

## Non-claims
- No claim that observability is redacted.
- No claim that telemetry sinks are safe.

## Client-ready summary
Tracing, masking, metrics, and telemetry files are present, but the review does not validate whether they actually redact sensitive data.

## Mapping table

| Mapping ID | Related risk ID/category | Related PHASE 6 threat ID | Related PHASE 5 architecture evidence | Candidate Onyx file/path | Mapping label | Why this file/path matters | Missing evidence | Later validation method | Notes |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| LOG-MAP-01 | LOG-01 / LOG-02 | TH-10 | logging_telemetry_map.md; backend_architecture.md; deployment_flow_map.md | backend/onyx/tracing/flows.py; backend/onyx/tracing/llm_utils.py; backend/onyx/tracing/setup.py | EXISTING-CANDIDATE | These tracing setup and flow files appear to control observability spans and LLM-related trace propagation. | No live log or telemetry sink inspection was performed. | Trace-content and log-redaction validation. | Potential observability control point. |
| LOG-MAP-02 | LOG-03 / LOG-04 / PI-05 | TH-10 / TH-13 / TH-15 | logging_telemetry_map.md; backend_architecture.md; deployment_flow_map.md | backend/onyx/tracing/masking.py; backend/onyx/tracing/framework/spans.py; backend/onyx/tracing/framework/traces.py; backend/onyx/tracing/langfuse_tracing_processor.py; backend/ee/onyx/utils/telemetry.py | EXISTING-CANDIDATE | These files suggest masking and telemetry processing paths where sensitive data could be redacted or exported. | No runtime proof of redaction or telemetry filtering was collected. | Sensitive-field redaction and telemetry-content review. | Relevant to logs, traces, and third-party telemetry. |
| LOG-MAP-03 | LOG-05 | TH-10 | logging_telemetry_map.md; backend_architecture.md | backend/onyx/tracing/masking.py; backend/onyx/server/metrics/metrics_server.py; backend/onyx/tracing/langfuse_tracing_processor.py | MISSING-CANDIDATE | The review found masking and metrics code, but no dedicated evidence path proving end-to-end redaction or sink filtering for sensitive fields. | No dedicated redaction-proof or telemetry-content validation was found in this pass. | Redaction proof review and telemetry-sink inspection. | Evidence gap, not a claim that redaction is absent. |
