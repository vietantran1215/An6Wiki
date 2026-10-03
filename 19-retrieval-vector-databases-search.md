# Retrieval, Vector Databases & Search

## BM25 vs dense retrieval

BM25 is strong for exact evidence such as:

- identifiers;
- error messages;
- product names;
- code symbols;
- rare domain terms.

Dense retrieval is strong for semantic similarity.

Hybrid retrieval combines both.

## Production retrieval pipeline

```text
BM25 candidates
      \
       → fusion → reranker → context builder
      /
Dense candidates
```

The first stage maximizes recall. The reranker spends more compute on fewer candidates to improve precision.

## Vector-store decision dimensions

Evaluate:

- scale;
- metadata filtering;
- hybrid search;
- operational burden;
- latency;
- multi-tenancy;
- freshness;
- cost;
- cloud coupling;
- ecosystem.

## Common options

### pgvector

Strong when PostgreSQL is already part of the platform and vector scale is moderate.

### OpenSearch

Strong when lexical + vector hybrid retrieval and search infrastructure matter.

### Pinecone

Managed vector-first option when minimizing operations is valuable.

### Qdrant

Vector-first engine with strong filtering and self-host/managed deployment options.

### Chroma

Useful for local development, learning, prototypes, and smaller workloads.

## Vectorless retrieval

Not every retrieval problem requires vectors.

Alternatives include:

- SQL;
- full-text search;
- graph traversal;
- tree reasoning;
- exact indexes.

Choose the retrieval mechanism based on information structure and query behavior.
