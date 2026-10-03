# Architecture Decision Records

## Purpose

An ADR makes important decisions inspectable and revisitable.

## Template

```md
# ADR-012: Use OpenSearch for hybrid retrieval

## Context
We need lexical + dense retrieval over 500k documents with metadata filtering.

## Decision
Use OpenSearch as the production retrieval engine.

## Alternatives
- pgvector
- Pinecone
- Qdrant

## Trade-offs
Pros:
- BM25 + vector in one engine
- mature filtering/search operations

Cons:
- heavier operations
- more cluster tuning

## Consequences
The platform team owns OpenSearch operations and index lifecycle.

## Revisit when
Vector corpus or operational cost changes materially.
```

## Good ADR characteristics

- concrete context;
- alternatives considered;
- explicit trade-offs;
- decision date;
- owner;
- revisit condition.

## Anti-pattern

An ADR should not pretend the chosen option has no downside.

The purpose is to preserve reasoning, not justify a preselected answer.
