> This is the client-facing mirror of the PHASE 7 evidence file. The canonical evidence copy remains under rag-security-readiness-review/02_evidence/phase_7/.

# RAG Risks

## Category purpose

Organize retrieval, search, answer-generation, and citation risks.

## Scope

Search, chat, retrieval, indexing, citation/source integrity, and multi-tenant retrieval paths.

## Related PHASE 5 architecture evidence

- rag-security-readiness-review/02_evidence/phase_5/rag_pipeline_map.md
- rag-security-readiness-review/02_evidence/phase_5/api_routes_map.md
- rag-security-readiness-review/02_evidence/phase_5/authorization_flow_map.md
- rag-security-readiness-review/02_evidence/phase_5/backend_architecture.md

## Related PHASE 6 threats

- TH-01
- TH-02
- TH-06
- TH-08
- TH-09

## Protected assets affected

Document contents; retrieved chunks; search indexes; citation/source references; tenant context

## Actors involved

Authenticated user; compromised user; malicious insider; compromised connector account

## Trust boundaries involved

Retrieval/search; authorization; tenant/group; chunking/indexing

## Data flows involved

User query to retrieval and answer generation; connector ingestion to index population; citation/source return to client

## Risk list

| Risk ID | Risk | Evidence label | Related PHASE 6 threat ID | Related PHASE 5 evidence | Affected assets | Actors | Trust boundaries | Potential impact | Missing evidence | Later validation method | Priority |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| RAG-01 | Unauthorized retrieval of private documents; sensitive data returned through search/chat. | EVIDENCE-LINKED | TH-01 | rag_pipeline_map.md; api_routes_map.md; authorization_flow_map.md; backend_architecture.md | Document contents; retrieved chunks; search indexes; citation/source references; tenant context | Authenticated user; compromised user; malicious insider; compromised connector account | Retrieval/search; authorization; tenant/group; chunking/indexing | Sensitive source disclosure through retrieval or chat output. | No runtime authz test or live search-result review. | Later integration or route-authz review. | Critical candidate |
| RAG-02 | Cross-tenant or cross-group retrieval; missing retrieval authorization evidence. | INFERRED | TH-02 | rag_pipeline_map.md; api_routes_map.md; authorization_flow_map.md; backend_architecture.md | Document contents; retrieved chunks; search indexes; citation/source references; tenant context | Authenticated user; compromised user; malicious insider; compromised connector account | Retrieval/search; authorization; tenant/group; chunking/indexing | Cross-tenant data exposure or group leakage. | No live tenant state review. | Later multi-tenant isolation review. | High candidate |
| RAG-03 | Retrieval poisoning and RAG quality failure can distort search results. | INFERRED | TH-09 | rag_pipeline_map.md; api_routes_map.md; authorization_flow_map.md; backend_architecture.md | Document contents; retrieved chunks; search indexes; citation/source references; tenant context | Authenticated user; compromised user; malicious insider; compromised connector account | Retrieval/search; authorization; tenant/group; chunking/indexing | Misleading results, hidden content, or degraded answer quality. | No live index manipulation test. | Later search-integrity review. | Medium candidate |
| RAG-04 | Incomplete citation/source integrity can undermine provenance trust. | UNVERIFIED | TH-08 | rag_pipeline_map.md; api_routes_map.md; authorization_flow_map.md; backend_architecture.md | Document contents; retrieved chunks; search indexes; citation/source references; tenant context | Authenticated user; compromised user; malicious insider; compromised connector account | Retrieval/search; authorization; tenant/group; chunking/indexing | Users may trust false or misleading provenance. | No citation-rendering validation. | Later citation-integrity review. | Medium candidate |
| RAG-05 | Over-indexing of private data can expand the retrieval blast radius. | INFERRED | TH-06 | rag_pipeline_map.md; api_routes_map.md; authorization_flow_map.md; backend_architecture.md | Document contents; retrieved chunks; search indexes; citation/source references; tenant context | Authenticated user; compromised user; malicious insider; compromised connector account | Retrieval/search; authorization; tenant/group; chunking/indexing | More private data becomes searchable or retrievable than intended. | No live sync scope review. | Later connector-scope and indexing review. | Medium candidate |

## Missing evidence

No runtime retrieval authorization test; no live search-result or citation-rendering validation; no live index manipulation or tenant-state review.

## Later validation methods

Route-level integration review for retrieval authz; live tenant isolation review; citation/source integrity review; search-integrity and index-poisoning review.

## Non-claims

No claim of exploitability; no claim that retrieval controls are verified; no claim of production readiness.

## Client-ready summary

The category links search and chat exposure risks to repository-backed retrieval and citation surfaces while preserving the source-only limitation.
