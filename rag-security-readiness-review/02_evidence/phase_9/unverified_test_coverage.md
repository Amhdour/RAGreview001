# Unverified Test Coverage

| Coverage ID | Category | Related control/risk | Existing file | Why coverage is unverified | Missing assertion/evidence | Later validation method |
|---|---|---|---|---|---|---|
| UNVERIFIED-001 | Authentication | Auth review coverage / AUTH-01, AUTH-02 | `rag-security-readiness-review/02_evidence/phase_9/authentication_review/auth_tests_review.md` | It is a review artifact, not an execution record. | No pass/fail output or runtime proof. | Run targeted auth tests and capture output. |
| UNVERIFIED-002 | Retrieval ACL | ACL filtering / ACL-01, ACL-02 | `backend/tests/unit/onyx/access/test_user_file_access.py` | The filename suggests access control, but not search-time retrieval ACL enforcement. | No assertion proving retrieval filtering. | Add or run integration retrieval ACL checks. |
| UNVERIFIED-003 | Prompt/context | Prompt safety / PI-01, PI-02 | `backend/tests/unit/onyx/chat/test_citation_processor.py` | The file covers citation processing, not adversarial prompt handling. | No prompt-injection assertion. | Run prompt-safety regression tests. |
| UNVERIFIED-004 | Agent/tool/MCP | MCP OAuth / AGENT-01, AGENT-02 | `web/tests/e2e/mcp/mcp_oauth_flow.spec.ts` | The spec exists on disk but was not executed. | No browser execution or result artifact. | Run the Playwright MCP OAuth flow. |
| UNVERIFIED-005 | Logging/telemetry | Tracing flow registry / LOG-01, LOG-02 | `backend/tests/unit/onyx/tracing/test_flows_registry.py` | The file exists, but this pass did not execute it or verify emitted traces. | No trace output or test result. | Run targeted tracing tests. |
