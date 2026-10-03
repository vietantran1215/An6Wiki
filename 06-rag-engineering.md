# RAG Engineering

## 1. What is RAG?

Retrieval-Augmented Generation separates retrieval from generation.

```text
Documents
 → ingest
 → clean
 → chunk
 → embed/index
 → retrieve
 → rerank
 → build context
 → prompt
 → LLM
 → answer + citations
```

## 2. Retrieval families

- BM25 / lexical;
- dense vector;
- metadata filtering;
- SQL;
- graph traversal;
- tree/reasoning-based;
- web/tool;
- multimodal.

## 3. Hybrid retrieval

Dense retrieval captures semantic similarity. BM25 captures exact lexical evidence.

```text
dense candidates
      \
       → fusion (e.g. RRF) → reranker → context builder
      /
BM25 candidates
```

## 4. Chunking

Strategies include fixed-size, recursive, semantic, sentence-window, parent-child, document-structure-aware, code-aware, AST-based, and multimodal/page-layout-aware.

Choose based on source structure and retrieval task.

## 5. Advanced patterns

Query rewriting, multi-query, step-back, HyDE, sub-question decomposition, Corrective RAG, Adaptive RAG, Self-RAG, Agentic RAG, GraphRAG, RAPTOR, iterative retrieval, vectorless retrieval, and multimodal RAG.

## 6. Permission-aware retrieval

```text
Authenticated principal
 → authorization context
 → permission-aware retriever
 → authorized documents only
 → secure context builder
 → LLM
```

Never use a user-provided metadata filter as the source of authorization truth.

## 7. Quality

Evaluate retrieval precision/recall, reranking, context quality, faithfulness, answer relevance, citation correctness, latency, tokens, cost, freshness, and permission leakage.

## 8. Minimal RRF

```python
from collections import defaultdict

def rrf(*rankings: list[str], k: int = 60) -> list[str]:
    # RRF combines result rankings without requiring
    # score calibration between retrievers.
    score = defaultdict(float)

    for ranking in rankings:
        for rank, doc_id in enumerate(ranking, start=1):
            score[doc_id] += 1.0 / (k + rank)

    return sorted(score, key=score.get, reverse=True)
```
