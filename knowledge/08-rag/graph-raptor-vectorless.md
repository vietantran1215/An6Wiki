# GraphRAG, RAPTOR & Vectorless RAG

## GraphRAG

Graph-based retrieval models entities and relationships.

Useful when questions depend on:

- multi-hop relationships;
- organizational dependencies;
- entity neighborhoods;
- community/global summaries.

Pipeline may include:

```text
documents
 → entity/relation extraction
 → graph construction
 → community/summary generation
 → graph-aware retrieval
```

Costs:

- extraction quality;
- graph update complexity;
- entity resolution;
- additional storage;
- query planning.

## RAPTOR

RAPTOR-style approaches recursively cluster/summarize content into a hierarchy.

Useful for questions at multiple abstraction levels.

Risk: summary hierarchy can introduce information loss or generated inaccuracies.

## Vectorless RAG

Vectorless retrieval uses non-vector mechanisms:

- BM25/full-text;
- SQL;
- graph traversal;
- tree/hierarchy;
- metadata;
- symbolic indexes.

## Decision framework

Use GraphRAG when relationships are first-class.

Use hierarchical retrieval when global and local abstraction levels matter.

Use vectorless approaches when source structure/query semantics are explicit enough that dense similarity adds little value.

## Rule

"RAG" means retrieval-augmented generation, not "vector database + LLM."
