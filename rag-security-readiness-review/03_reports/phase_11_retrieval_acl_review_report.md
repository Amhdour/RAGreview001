# PHASE 11 Retrieval ACL Review Report

## Executive summary
PHASE 11 created a source-only retrieval ACL evidence package that traces how user, group, tenant, document-set, source, tag, time, persona, project, and attached-document inputs flow through search preprocessing and into Vespa and OpenSearch retrieval builders. The review is COMPLETE WITH LIMITATIONS because runtime ACL enforcement, tests, CI, and production behavior were not validated.

## Evidence basis
This report is based on the current checkout plus PHASE 10, PHASE 9, PHASE 8, PHASE 7, PHASE 6, PHASE 5, and PHASE 3 evidence files. No runtime, CI, production, exploit, customer-data, or real-secret evidence was used.

## Retrieval entry point summary
Search reaches the backend through `POST /api/search`, the Onyx Search UI backend, admin search, chat message handling, and frontend helpers that call the search endpoints. These are the entry points that matter for retrieval ACL review.

## Search preprocessing summary
Search preprocessing validates the request, normalizes the time cutoff to UTC, materializes persona and document-set context, optionally applies query expansion, and converts request fields into `BaseFilters`/`IndexFilters` objects.

## ACL filter construction summary
ACL filters are constructed from user identity, public access, group-aware access, document-set access, tenant ID, source type, tags, time cutoff, persona/project/attached-document scope, and connector status. Vespa and OpenSearch each receive backend-specific filter expressions.

## ACL input summary
Observed ACL inputs include user identity, user role, groups, tenant ID, document sets, source type, tags, persona/project/attached-doc scope, connector status, and permission-sync timestamps. Workspace-specific retrieval scope was not separately identified in the inspected source.

## Vector / keyword filtering summary
Both Vespa and OpenSearch expose keyword, semantic/vector, and hybrid retrieval builders. The source shows ACL filters being carried into these builders, but runtime filtering correctness was not validated.

## Reranking assumptions summary
The code fans out to multiple retrieval functions, merges or fuses ranked results, and only later performs LLM-based selection and section expansion. That is a source-level ordering observation, not runtime proof.

## Bypass-prone path summary
Direct document-ID retrieval, admin search, citation/source rendering, permission-sync paths, and history-reuse paths were reviewed as possible bypass or exposure edges. None were runtime-validated in this phase.

## Deleted/stale document handling summary
Deletion- and staleness-aware hooks exist in document access, permission-sync, and stale-group cleanup code. The actual lag between a source permission change and search visibility update remains unverified.

## Cross-user/group/connector risk summary
The source shows explicit user, group, connector, and public/shared access logic. Cross-user, cross-group, cross-tenant, cross-workspace, and cross-connector leakage risks remain unverified without runtime evidence.

## Retrieval ACL test summary
Relevant test files and evidence artifacts were discovered, including search-permission and document-set permission tests, but they were not executed.

## Confirmed findings
- Source-level retrieval ACL filters are constructed before retrieval dispatch.
- Document access predicates exclude deleting connector pairs and use public/email/group-based access checks.
- OpenSearch carries ACL and scope filters into keyword, semantic, and hybrid search queries.
- Vespa builds ACL filters and applies post-query ACL checks in its document-by-ID retrieval path.

## Observations
- Search, chat, admin, and frontend helpers all contribute to retrieval entry points.
- Search tool reranking and selection happen after retrieval fan-out.
- Citation rendering uses returned document metadata.
- Search history is stored per user.

## Unverified risks
- Runtime ACL enforcement is not proven.
- Direct-ID retrieval assumes prior validation.
- Permission-sync lag and stale-state effects are not measured.
- Citation/source metadata exposure is not tested.

## Missing evidence
No test run output, CI output, runtime trace, production evidence, or live state evidence was collected.

## Limitations
Source-only review; current checkout only; original source unavailable; working copy unavailable; tests discovered but not executed; CI not executed; runtime, production, and live-state behavior not validated.

## Non-claims
This report does not claim production readiness, effective ACL enforcement, test success, exploitability, or completeness of runtime coverage.

## PHASE 11 status
COMPLETE WITH LIMITATIONS

## Exact next phase
PHASE 12 — Review document ingestion security
