
# Citation/Source Findings

## Confirmed findings

### F-14-01 — Missing citation targets are skipped, not fabricated
- Status: CONFIRMED-FINDING
- Evidence: `backend/onyx/chat/citation_processor.py:484-503`; `backend/onyx/chat/citation_utils.py:201-207`
- What is confirmed: The citation processor warns on unknown citation numbers and skips them; citation renumbering preserves unmatched numbers rather than inventing new sources.
- What is not confirmed: Whether runtime answer generation always avoids implying support from omitted citations.
- Security relevance: A missing or malformed citation is not silently replaced with a fabricated source.
- Client-ready wording: The backend does not appear to invent missing citation targets; unknown citations are skipped.

### F-14-02 — Backend citation mapping and frontend source display are separate layers
- Status: CONFIRMED-FINDING
- Evidence: `backend/onyx/chat/llm_loop.py:650-663,692-1074`; `web/src/components/search/results/Citation.tsx:67-123`; `web/src/refresh-components/buttons/source-tag/SourceTag.tsx:267-555`
- What is confirmed: Citation mapping is built in the backend and the frontend renders source labels and tooltips from document metadata.
- What is not confirmed: That the rendered label is always authoritative or access-checked at display time.
- Security relevance: A display-layer label can diverge from source identity if upstream metadata is stale or misleading.
- Client-ready wording: The code separates backend citation mapping from frontend source display.

## Observations

### O-14-01
- Status: OBSERVATION
- Evidence: `backend/onyx/context/search/models.py:244-307`; `backend/onyx/tools/tool_implementations/utils.py:29-118`
- Meaning: Source identity, title, URL, metadata, and document IDs are carried through search and tool-response structures.
- Limitation: This does not prove the data is correct at runtime.

### O-14-02
- Status: OBSERVATION
- Evidence: `backend/onyx/connectors/web/connector.py:419-604`; `backend/onyx/db/document.py:667-716`
- Meaning: Connector-derived titles, links, and metadata are persisted into the document layer.
- Limitation: No live connector-state validation was performed.

### O-14-03
- Status: OBSERVATION
- Evidence: `web/src/components/search/DocumentDisplay.tsx:130-156`; `web/src/components/search/results/Citation.tsx:67-123`; `web/src/refresh-components/buttons/source-tag/SourceTagDetailsCard.tsx:114-176`
- Meaning: The frontend renders source labels, icons, and tooltips from the incoming source metadata.
- Limitation: Rendering logic is not an authorization check.

### O-14-04
- Status: OBSERVATION
- Evidence: `backend/onyx/db/models.py:963-1055,3409-3458`
- Meaning: Document and document-set models store semantic identifiers, links, file IDs, metadata, and access scope.
- Limitation: Persisted fields do not prove freshness or trustworthiness.

### O-14-05
- Status: OBSERVATION
- Evidence: `backend/onyx/chat/citation_processor.py:215-247,324-531`; `backend/onyx/chat/citation_utils.py:100-221`
- Meaning: Citation handling is deterministic and map-driven, with explicit renumbering and formatting logic.
- Limitation: Runtime end-to-end correctness was not validated.

## Unverified risks

### R-14-01 — Citation spoofing remains unverified
- Status: UNVERIFIED-RISK
- Why unverified: No runtime proof shows the UI or backend blocks crafted source labels or citation-like content from appearing deceptive.
- Missing evidence: Executed tests or runtime traces for adversarial source metadata.
- Later validation method: Run controlled source-metadata spoofing tests in a sandbox.
- Client-ready wording: Source labels may still be misleading under adversarial metadata.

### R-14-02 — Misleading source attribution remains unverified
- Status: UNVERIFIED-RISK
- Why unverified: The review found no execution evidence proving title, URL, connector, and chunk data always stay aligned.
- Missing evidence: Runtime source reconciliation and stale-update checks.
- Later validation method: Compare rendered labels to canonical document records in integration tests.
- Client-ready wording: A displayed source may not always match the underlying document identity.

### R-14-03 — Stale or deleted source display remains unverified
- Status: UNVERIFIED-RISK
- Why unverified: No post-delete or post-update runtime source-display evidence was collected.
- Missing evidence: Live deletion, refresh, and session-reload validation.
- Later validation method: Exercise delete/update flows and inspect rendered source cards.
- Client-ready wording: Old source labels could remain visible after document or connector changes.

### R-14-04 — Inaccessible source display remains unverified
- Status: UNVERIFIED-RISK
- Why unverified: No runtime ACL recheck before source rendering was observed or executed.
- Missing evidence: ACL-aware source-display tests.
- Later validation method: Compare source rendering for authorized and unauthorized users.
- Client-ready wording: A source may be visible even when the current user should not access it.

## No-evidence-found areas
- No executed citation/source integrity tests.
- No runtime source-display validation.
- No runtime ACL recheck validation before display.
- No production or live-state evidence.
