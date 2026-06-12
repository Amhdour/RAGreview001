# Reranking Assumptions

## Reranking files
- `backend/onyx/context/search/retrieval/search_runner.py`
- `backend/onyx/tools/tool_implementations/search/search_tool.py`
- `backend/onyx/tools/tool_implementations/search/search_utils.py`

## Reranking input candidates
- Search queries are fanned out across semantic, keyword, and federated paths in `search_tool.py`.
- The search runner combines results from multiple retrieval functions in `search_runner.py`.
- `weighted_reciprocal_rank_fusion` merges those candidate lists before later LLM selection.

## Whether reranking appears after initial retrieval
Source shows that reranking happens after retrieval fan-out, not before it. `search_runner.py` first retrieves chunks, then `search_tool.py` applies weighted reciprocal rank fusion, and only later does LLM-based document selection/section expansion.

## Whether ACL filtering appears before reranking
Source indicates that ACL filters are built before retrieval is dispatched and passed into each backend query. That is a source-level ordering fact, but it does not validate runtime enforcement.

## Whether reranker receives only authorized candidates
This remains UNVERIFIED. The code path is consistent with authorized-only candidate construction, but no runtime trace or test execution evidence was collected here.

## Runtime ordering assumptions
- Source-level ordering suggests ACL filters are applied during query construction.
- The search tool’s rank fusion and later LLM selection occur after retrieval results are returned.
- No runtime evidence proves that every backend honors the filters identically.

## Unverified risks
- A backend could ignore or misapply the filter object even though the source passes it through.
- Rank fusion could combine stale or unauthorized results if an upstream backend path is incomplete.
- LLM selection occurs after retrieval and therefore inherits whatever candidate set the retrieval layer already produced.
