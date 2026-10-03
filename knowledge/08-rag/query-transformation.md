# Query Transformation

## Why transform queries?

User wording may be:

- ambiguous;
- underspecified;
- conversational;
- too broad;
- mismatched with document vocabulary.

## Query rewriting

Rewrite into a search-oriented query.

Example:

```text
User: "why did it fail after deploy?"
Rewrite: "production deployment failure causes rollback incident"
```

## Multi-query

Generate multiple retrieval variants and fuse results.

Good for ambiguous questions, but increases retrieval cost.

## HyDE

Generate a hypothetical answer/document and embed that representation for retrieval.

Useful when the user's query is short but relevant documents are verbose.

## Step-back query

Generate a more general conceptual query before retrieval.

Useful for questions requiring broader background.

## Sub-question decomposition

Break multi-part questions into independent retrieval tasks.

```text
"Compare OpenSearch and pgvector for permission-aware hybrid RAG"

→ hybrid search capability?
→ permission filtering?
→ operational complexity?
→ cost/scale?
```

## Routing

Some queries should not use vector retrieval at all.

Possible routes:

- SQL;
- BM25;
- hybrid;
- graph;
- web;
- direct answer.

## Guardrails

Query transformation must not silently broaden authorization scope.

## Rule

Add query transformation when measured retrieval failures show query-document mismatch—not because advanced RAG diagrams include it.
