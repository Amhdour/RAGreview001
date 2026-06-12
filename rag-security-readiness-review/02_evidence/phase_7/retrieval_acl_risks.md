# Retrieval ACL Risks

## Category purpose

Track document-level ACL and indexing risks that can let search or citations surface restricted content.

## Scope

ACL enforcement on document retrieval, connector sync, deletion, and citation/source handling.

## Related PHASE 5 architecture evidence

- rag-security-readiness-review/02_evidence/phase_5/rag_pipeline_map.md
- rag-security-readiness-review/02_evidence/phase_5/authorization_flow_map.md
- rag-security-readiness-review/02_evidence/phase_5/data_model_map.md
- rag-security-readiness-review/02_evidence/phase_5/api_routes_map.md

## Related PHASE 6 threats

- TH-01
- TH-02
- TH-03
- TH-05
- TH-06
- TH-08

## Protected assets affected

Document ACLs; connector sync state; index entries; deleted/restricted content state; citation metadata

## Actors involved

Authenticated user; compromised user; compromised connector account; malicious insider

## Trust boundaries involved

Document-level ACL; connector/external system; tenant/group; retrieval/search

## Data flows involved

Connector sync into index; document retrieval to answer generation; citation/source display

## Risk list

| Risk ID | Risk | Evidence label | Related PHASE 6 threat ID | Related PHASE 5 evidence | Affected assets | Actors | Trust boundaries | Potential impact | Missing evidence | Later validation method | Priority |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| ACL-01 | Missing or inconsistent document-level ACL enforcement can let search surface restricted content. | EVIDENCE-LINKED | TH-01, TH-03 | rag_pipeline_map.md; authorization_flow_map.md; data_model_map.md; api_routes_map.md | Document ACLs; connector sync state; index entries; deleted/restricted content state; citation metadata | Authenticated user; compromised user; compromised connector account; malicious insider | Document-level ACL; connector/external system; tenant/group; retrieval/search | Restricted documents may appear in search or chat. | No live document-ACL enforcement check. | Later ACL enforcement review. | Critical candidate |
| ACL-02 | Stale connector permissions can cause search results to reflect outdated access rights. | INFERRED | TH-05, TH-06 | rag_pipeline_map.md; authorization_flow_map.md; data_model_map.md; api_routes_map.md | Document ACLs; connector sync state; index entries; deleted/restricted content state; citation metadata | Authenticated user; compromised user; compromised connector account; malicious insider | Document-level ACL; connector/external system; tenant/group; retrieval/search | Previously revoked or changed permissions may remain effective in the index. | No live connector-permission sync review. | Later permission-sync review. | High candidate |
| ACL-03 | Overbroad connector sync permissions may ingest content outside intended scope. | INFERRED | TH-05, TH-06 | rag_pipeline_map.md; authorization_flow_map.md; data_model_map.md; api_routes_map.md | Document ACLs; connector sync state; index entries; deleted/restricted content state; citation metadata | Authenticated user; compromised user; compromised connector account; malicious insider | Document-level ACL; connector/external system; tenant/group; retrieval/search | The indexed corpus can include more sensitive source material than intended. | No live sync-scope review. | Later connector-scope review. | High candidate |
| ACL-04 | Cross-user retrieval leakage can expose another user’s private documents. | EVIDENCE-LINKED | TH-01, TH-02 | rag_pipeline_map.md; authorization_flow_map.md; data_model_map.md; api_routes_map.md | Document ACLs; connector sync state; index entries; deleted/restricted content state; citation metadata | Authenticated user; compromised user; compromised connector account; malicious insider | Document-level ACL; connector/external system; tenant/group; retrieval/search | A user may see content not owned or shared with them. | No live search-result authorization test. | Later cross-user retrieval review. | High candidate |
| ACL-05 | Citation output may expose inaccessible source metadata even when content is blocked. | UNVERIFIED | TH-08 | rag_pipeline_map.md; authorization_flow_map.md; data_model_map.md; api_routes_map.md | Document ACLs; connector sync state; index entries; deleted/restricted content state; citation metadata | Authenticated user; compromised user; compromised connector account; malicious insider | Document-level ACL; connector/external system; tenant/group; retrieval/search | Users may infer existence or location of protected sources. | No citation privacy validation. | Later citation-privacy review. | Medium candidate |

## Missing evidence

No live document-ACL enforcement check; no live connector permissions review; no live index-retention review for deleted or restricted items.

## Later validation methods

ACL enforcement validation; connector permissions and sync-scope review; index-retention and citation privacy review.

## Non-claims

No claim that document ACLs are correct; no claim that citations only expose accessible sources; no claim that deleted content is purged from the index.

## Client-ready summary

The category focuses on content that should be hidden but may still be reachable through retrieval or provenance metadata.
