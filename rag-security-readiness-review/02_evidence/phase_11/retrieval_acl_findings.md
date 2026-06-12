# Retrieval ACL Findings

## Confirmed findings

### FINDING-11-001
- **Finding title:** Source-level retrieval ACL filters are constructed before retrieval dispatch.
- **Status:** CONFIRMED-FINDING.
- **Evidence:** `backend/onyx/context/search/pipeline.py:69-147`, `backend/onyx/server/features/search/api.py:58-147`, `backend/onyx/tools/tool_implementations/search/search_tool.py:554-635`, `backend/onyx/context/search/retrieval/search_runner.py:90-166`.
- **What is confirmed:** Search and chat-adjacent retrieval paths build `IndexFilters` with ACL, tenant, source, document-set, tag, and time inputs, then pass them into retrieval functions.
- **What is not confirmed:** Runtime enforcement, backend-specific result correctness, and end-to-end authorization.
- **Security relevance:** This is the main source-level retrieval ACL construction path.
- **Client-ready wording:** The code constructs retrieval ACL filters before search execution, but runtime enforcement was not validated in this phase.

### FINDING-11-002
- **Finding title:** Document access predicates exclude deleting connector pairs and require explicit public or overlap-based access.
- **Status:** CONFIRMED-FINDING.
- **Evidence:** `backend/onyx/db/document_access.py:31-88`.
- **What is confirmed:** Search-time document access logic admits only public connectors, public documents, email matches, or group overlap, while excluding `DELETING` connector pairs.
- **What is not confirmed:** That every search backend path relies on this predicate at runtime.
- **Security relevance:** This is the core source-level document access rule.
- **Client-ready wording:** Document access logic is explicitly permission-aware in source, but the live effect of that logic was not verified here.

### FINDING-11-003
- **Finding title:** OpenSearch retrieval queries carry ACL and scope filters into keyword, semantic, and hybrid search.
- **Status:** CONFIRMED-FINDING.
- **Evidence:** `backend/onyx/document_index/opensearch/search.py:315-582`, `backend/onyx/document_index/opensearch/search.py:1197-1296`.
- **What is confirmed:** OpenSearch search builders include ACL, source, tag, knowledge-scope, time, and tenant filters in the query body.
- **What is not confirmed:** That query results were executed or validated in a live environment.
- **Security relevance:** This is the main OpenSearch retrieval filter construction path.
- **Client-ready wording:** The OpenSearch query builders are ACL-aware in source, but runtime proof is still missing.

### FINDING-11-004
- **Finding title:** Vespa retrieval builds ACL filters and performs post-query ACL checks in at least one retrieval path.
- **Status:** CONFIRMED-FINDING.
- **Evidence:** `backend/onyx/document_index/vespa/shared_utils/vespa_request_builders.py:30-252`, `backend/onyx/document_index/vespa/vespa_document_index.py:892-980`, `backend/onyx/document_index/vespa/chunk_retrieval.py:203-289`.
- **What is confirmed:** Vespa query construction includes ACL filter materialization, and the document-by-ID retrieval path applies ACL checks after retrieval because Vespa selection cannot directly use ACL `contains` logic.
- **What is not confirmed:** That the full runtime search path always evaluates ACLs before user-visible ranking or selection.
- **Security relevance:** This is the main Vespa retrieval ACL construction path.
- **Client-ready wording:** Vespa retrieval is ACL-aware in source, but the runtime ordering and enforcement were not tested here.

## Observations

### OBS-11-001
- **Status:** OBSERVATION.
- **Evidence:** `backend/onyx/server/query_and_chat/chat_backend.py:528-620`, `backend/ee/onyx/server/query_and_chat/search_backend.py:51-140`, `web/src/ee/lib/search/svc.ts:17-95`.
- **Meaning:** Retrieval entry points exist in both backend and frontend layers, including chat-adjacent and search-specific flows.
- **Limitation:** Entry-point existence does not prove authorization correctness.

### OBS-11-002
- **Status:** OBSERVATION.
- **Evidence:** `backend/onyx/tools/tool_implementations/search/search_tool.py:754-981`.
- **Meaning:** Search results are fused and then further selected/expanded after retrieval.
- **Limitation:** The observed ordering is source-level only; no runtime traces were collected.

### OBS-11-003
- **Status:** OBSERVATION.
- **Evidence:** `web/src/components/search/results/Citation.tsx:37-121`.
- **Meaning:** The UI renders citation labels from returned document metadata and opens the associated document object.
- **Limitation:** This is not an ACL enforcement point.

### OBS-11-004
- **Status:** OBSERVATION.
- **Evidence:** `backend/onyx/db/search.py:12-64`.
- **Meaning:** Search history is stored per user and can be queried back for that same user.
- **Limitation:** Search history is not a retrieval ACL control.

## Unverified risks

### RISK-11-001
- **Status:** UNVERIFIED-RISK.
- **Why unverified:** No runtime, test, or CI evidence proves that all retrieval backends honor the constructed ACL filters exactly as intended.
- **Missing evidence:** Live search traces, ACL regression tests, and executed CI.
- **Later validation method:** Execute targeted negative search tests against known forbidden documents and compare backend behavior.
- **Client-ready wording:** Source-level ACL filters exist, but runtime enforcement has not been proven in this phase.

### RISK-11-002
- **Status:** UNVERIFIED-RISK.
- **Why unverified:** `inference_sections_from_ids()` assumes the IDs were already validated and disables ACL filtering locally.
- **Missing evidence:** Caller-chain validation and runtime tests for forbidden document IDs.
- **Later validation method:** Trace every caller and run a negative direct-ID retrieval test.
- **Client-ready wording:** A direct-ID retrieval helper relies on prior validation, which has not been runtime-tested here.

### RISK-11-003
- **Status:** UNVERIFIED-RISK.
- **Why unverified:** Permission-sync and stale-group cleanup are source-visible but the freshness window is not measured here.
- **Missing evidence:** Live permission-sync timing and post-change search observations.
- **Later validation method:** Change source permissions, wait for sync, and verify search visibility transitions.
- **Client-ready wording:** Permission updates may lag search visibility, but the actual lag was not measured in this phase.

### RISK-11-004
- **Status:** UNVERIFIED-RISK.
- **Why unverified:** Citation rendering and source metadata exposure were observed, but no forbidden-source UI test was run.
- **Missing evidence:** Executed citation/privacy test results.
- **Later validation method:** Open a forbidden source citation in a live session and verify it is not exposed.
- **Client-ready wording:** Citation metadata exposure remains unproven either way.

## No-evidence-found areas
- No explicit workspace-specific retrieval filter path was identified in the inspected search code.
- No executed retrieval ACL tests were identified for this phase.
- No live runtime evidence was collected for ACL enforcement, result redaction, or citation privacy.
