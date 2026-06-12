> This is the client-facing mirror of the PHASE 7 evidence file. The canonical evidence copy remains under rag-security-readiness-review/02_evidence/phase_7/.

# Connector Risks

## Category purpose

Capture risks in source-system authentication, permission scope, and sync behavior.

## Scope

Connector credentials, external source access, sync scope, and downstream indexing.

## Related PHASE 5 architecture evidence

- rag-security-readiness-review/02_evidence/phase_5/rag_pipeline_map.md
- rag-security-readiness-review/02_evidence/phase_5/auth_flow_map.md

## Related PHASE 6 threats

- TH-02
- TH-05
- TH-06
- TH-07

## Protected assets affected

Connector credentials; source-system data; sync state; external account permissions

## Actors involved

Connector service account; compromised connector account; deployment/operator role; malicious insider

## Trust boundaries involved

Connector credential; connector/external system; ingestion; tenant/group

## Data flows involved

External source access to connector; connector sync to index; permission sync into local state

## Risk list

| Risk ID | Risk | Evidence label | Related PHASE 6 threat ID | Related PHASE 5 evidence | Affected assets | Actors | Trust boundaries | Potential impact | Missing evidence | Later validation method | Priority |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| CONN-01 | Connector credential exposure can allow external source compromise or over-sync. | EVIDENCE-LINKED | TH-05 | rag_pipeline_map.md; auth_flow_map.md | Connector credentials; source-system data; sync state; external account permissions | Connector service account; compromised connector account; deployment/operator role; malicious insider | Connector credential; connector/external system; ingestion; tenant/group | Source-system exposure or ingestion abuse. | No secret-storage verification. | Later secret-handling review. | Critical candidate |
| CONN-02 | Overbroad connector permission scope can ingest data beyond intended boundaries. | INFERRED | TH-05, TH-06 | rag_pipeline_map.md; auth_flow_map.md | Connector credentials; source-system data; sync state; external account permissions | Connector service account; compromised connector account; deployment/operator role; malicious insider | Connector credential; connector/external system; ingestion; tenant/group | The indexed corpus can include more sensitive source material than intended. | No live connector scope review. | Later connector-scope review. | High candidate |
| CONN-03 | Stale permission sync can leave revoked access effective in the index. | INFERRED | TH-06, TH-02 | rag_pipeline_map.md; auth_flow_map.md | Connector credentials; source-system data; sync state; external account permissions | Connector service account; compromised connector account; deployment/operator role; malicious insider | Connector credential; connector/external system; ingestion; tenant/group | Users may retain access to content after upstream changes. | No live permission-sync review. | Later permission-sync review. | Medium candidate |
| CONN-04 | Untrusted source ingestion can import hostile content or poisoned documents. | EVIDENCE-LINKED | TH-07, TH-05 | rag_pipeline_map.md; auth_flow_map.md | Connector credentials; source-system data; sync state; external account permissions | Connector service account; compromised connector account; deployment/operator role; malicious insider | Connector credential; connector/external system; ingestion; tenant/group | Hostile content can travel into search, chat, or tool flows. | No live source trust review. | Later ingestion-trust review. | High candidate |
| CONN-05 | Connector sync of unauthorized documents can expand the corpus without policy approval. | INFERRED | TH-06, TH-05 | rag_pipeline_map.md; auth_flow_map.md | Connector credentials; source-system data; sync state; external account permissions | Connector service account; compromised connector account; deployment/operator role; malicious insider | Connector credential; connector/external system; ingestion; tenant/group | Unapproved content can become searchable or visible. | No live sync approval review. | Later sync-scope review. | High candidate |

## Missing evidence

No live connector validation; no secret-storage verification; no live scope or permission-sync review.

## Later validation methods

Connector credential handling review; connector scope and permission-sync validation; external source trust review.

## Non-claims

No claim that connector scope is safe; no claim that external source accounts are secure; no claim that unauthorized documents are excluded live.

## Client-ready summary

The category keeps connector exposure separate from generic retrieval because it starts at the external source boundary.
