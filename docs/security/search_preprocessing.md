> This is the client-facing mirror of the PHASE 11 retrieval ACL review file. The canonical evidence copy remains under rag-security-readiness-review/02_evidence/phase_11/.

# Search Preprocessing

| Preprocessing step | File/path | Line reference if available | Input | Output | ACL relevance | Evidence label | Limitation |
| ------------------ | --------- | --------------------------- | ----- | ------ | ------------- | -------------- | ---------- |
| Query validation | `backend/onyx/server/features/search/models.py` | `12-37` | Search query, source filters, document sets, tags, persona, provider/model, message history. | Validated `SearchRequest`. | Guards malformed input before retrieval. | CONFIRMED-FINDING | Validation is syntactic, not an ACL guarantee. |
| UTC normalization | `backend/onyx/server/features/search/api.py` | `126-147` | Naive or aware `time_cutoff`. | UTC-aware `BaseFilters.time_cutoff`. | Ensures downstream time filtering is consistent. | CONFIRMED-FINDING | Time filtering does not prove authorization. |
| Search UI keyword fallback | `backend/ee/onyx/server/query_and_chat/search_backend.py` | `106-140` | Search request and `hybrid_alpha`. | Keyword-only mode when the UI uses OpenSearch keyword search. | Affects which retrieval backend runs. | OBSERVATION | Backend choice is separate from ACL proof. |
| Search request to filter model | `backend/onyx/server/features/search/api.py` | `126-147` | Request sources, document sets, tags, and time cutoff. | `BaseFilters`. | Feeds source/type and metadata filters into retrieval. | CONFIRMED-FINDING | Only source-level construction is visible here. |
| Persona context extraction | `backend/onyx/server/features/search/api.py` | `64-89` | Persona document sets, attached documents, hierarchy nodes. | `PersonaSearchInfo`. | Restricts or widens retrieval scope for persona-backed search. | CONFIRMED-FINDING | Runtime permission effect is unverified. |
| Search tool query expansion | `backend/onyx/tools/tool_implementations/search/search_tool.py` | `647-850` | Message history, memories, user info, original query, LLM expansions. | Ranked search queries and search packets. | Query shaping affects retrieval but is not itself ACL logic. | OBSERVATION | Query expansion does not prove authorization. |
| Document-set access precheck | `backend/onyx/context/search/pipeline.py` | `69-87` | User-selected document sets. | Permission error or allowed list. | Prevents one user-supplied bypass path at the source level. | CONFIRMED-FINDING | No runtime enforcement evidence collected. |
