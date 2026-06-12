# Existing Tests and Evidence Index

| Area | Test/evidence file | Type | Related control/risk | What it appears to cover | Limitation |
|---|---|---|---|---|---|
| Authentication | `backend/tests/unit/onyx/auth/test_user_registration.py` | Unit test | Registration and verification control / AUTH-01, AUTH-02 | Disposable-email blocking, invite logic, and SSO bypass behavior. | Not executed in this pass. |
| Authentication | `rag-security-readiness-review/02_evidence/phase_9/authentication_review/auth_tests_review.md` | Evidence review | PHASE 9A authentication controls | Review of available auth tests and coverage notes. | Review evidence only; no runtime proof. |
| Authorization | `backend/tests/unit/onyx/auth/test_permissions.py` | Unit test | Permission resolution and dependency checks / AUTHZ-01, AUTHZ-02 | Permission inference and auth dependency helpers. | Not executed in this pass. |
| Retrieval ACL | `backend/tests/integration/multitenant_tests/syncing/test_search_permissions.py` | Integration test | Search permission synchronization / ACL-01, ACL-02 | Search-permission syncing across tenants. | Not executed in this pass. |
| Ingestion | `backend/tests/unit/onyx/background/celery/tasks/test_user_file_processing_no_vectordb.py` | Unit test | User-file processing / RAG-03, RAG-05 | Ingestion-task behavior around file processing and vector-store exclusions. | Not executed in this pass. |
| Prompt/context | `backend/tests/unit/onyx/chat/test_citation_processor.py` | Unit test | Citation and context assembly / PI-01, PI-02 | Citation-processing logic used in chat answers. | Not executed and does not prove prompt-injection resistance. |
| Connector | `backend/tests/external_dependency_unit/tools/test_oauth_token_manager.py` | External dependency unit test | OAuth token refresh and connector credentials / CONN-01, CONN-02 | OAuth token management and refresh behavior. | Not executed in this pass. |
| Agent/tool/MCP | `backend/tests/unit/onyx/server/features/mcp/test_per_user_listing_invariants.py` | Unit test | MCP listing invariants / AGENT-01, AGENT-02 | Per-user listing invariants and auth template behavior. | Not executed in this pass. |
| Logging/telemetry | `backend/tests/unit/onyx/tracing/test_flows_registry.py` | Unit test | Tracing flow registry / LOG-01, LOG-02 | Flow registry and untagged sentinel definitions. | Not executed in this pass. |
| Deployment/CI | `backend/tests/unit/onyx/configs/test_sentry.py` | Unit test | Deployment/observability config / DEP-01, DEP-02 | Sentry instance-tagging and config behavior. | Not a CI workflow execution proof. |
| Deployment/CI | `docs/security/deployment_ci_risk_to_code.md` | Evidence file | Deployment/CI mapping evidence / DEP-01, DEP-02 | Source mapping evidence for deployment controls. | Evidence only; no pipeline execution. |
