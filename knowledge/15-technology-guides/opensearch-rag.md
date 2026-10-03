# OpenSearch for Production RAG

## Why OpenSearch is attractive

OpenSearch can combine:

- BM25;
- vector search;
- metadata filtering;
- aggregations;
- production search operations.

This makes it useful for hybrid RAG.

## Conceptual index

```json
{
  "document_id": "doc-123",
  "chunk_id": "doc-123#7",
  "text": "...",
  "embedding": [0.1, 0.2],
  "tenant_id": "tenant-a",
  "project_id": "project-x",
  "updated_at": "..."
}
```

## Retrieval

Run lexical and dense candidate search, fuse, then rerank.

## Permission filtering

Tenant/project/ACL filters must be applied during retrieval.

## Operations

Plan:

- shard/index sizing;
- refresh behavior;
- index versioning;
- reindex;
- snapshot/restore;
- monitoring;
- cost.

## Rule

OpenSearch is compelling when search itself is a core platform capability. If you only need modest vector lookup and already run PostgreSQL, pgvector may be simpler.
