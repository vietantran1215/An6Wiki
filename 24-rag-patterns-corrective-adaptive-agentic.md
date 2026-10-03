# RAG Patterns: Corrective, Adaptive, Agentic, Graph and Vectorless

## Baseline RAG

A single retrieval path:

```text
query → retrieve → generate
```

Good for predictable knowledge sources and low-complexity queries.

## Corrective RAG

Corrective RAG evaluates retrieved evidence before generation.

A simplified flow:

```text
query
 → retrieve
 → grade evidence
 ├─ sufficient → generate
 └─ weak → rewrite / alternate retrieval / web search
```

Use when retrieval quality is variable and the system can detect weak evidence.

## Adaptive RAG

Adaptive RAG routes different query types to different retrieval strategies.

Example:

```text
query
 → classify
 ├─ factual lookup → lexical/hybrid search
 ├─ analytical → multi-query + reranking
 ├─ structured data → SQL
 └─ no retrieval needed → direct generation
```

Use when one retrieval pipeline is inefficient across heterogeneous tasks.

## Agentic RAG

Agentic RAG lets the runtime repeatedly choose actions based on current state.

Possible actions:

- retrieve;
- rewrite;
- decompose;
- use a tool;
- inspect evidence;
- ask for clarification;
- stop.

Every loop must be bounded by explicit step, time, token, and cost limits.

## GraphRAG

GraphRAG uses graph structure to retrieve or reason over entities and relationships.

Strong when the question depends on:

- multi-hop relationships;
- connected entities;
- community/global summaries;
- relationship-heavy domains.

It adds graph construction, extraction quality, update, and operational cost.

## Vectorless RAG

Vectorless RAG uses another retrieval mechanism as the primary path.

Examples:

- full-text search;
- SQL;
- graph traversal;
- tree reasoning;
- metadata indexes.

Useful when source structure is explicit and semantic vector similarity adds little value.

## Decision sequence

1. Start with a simple baseline.
2. Measure retrieval failures.
3. Identify the failure class.
4. Add only the mechanism that addresses that failure.
5. Re-evaluate end-to-end and component metrics.

Do not add an "advanced RAG" label without an observed retrieval problem.
