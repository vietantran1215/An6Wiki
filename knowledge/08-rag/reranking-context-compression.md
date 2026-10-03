# Reranking & Context Compression

## Two-stage retrieval

A production retrieval system often separates:

1. cheap high-recall retrieval;
2. expensive high-precision reranking.

```text
100 candidates
 → reranker
 → top 10
 → context builder
```

## Rerankers

Possible approaches:

- cross-encoder;
- LLM scoring;
- provider reranking model;
- rule + model hybrid.

## Why reranking helps

Embedding similarity is approximate.

A stronger model can inspect query-document interaction more directly.

## Context compression

After retrieval, remove irrelevant content before prompting.

Techniques:

- select relevant sentences;
- extract evidence spans;
- deduplicate chunks;
- merge overlapping chunks;
- summarize only when provenance is preserved.

## Example evidence selection

```python
def select_top_chunks(scored_chunks, max_chunks=8):
    # Stable deterministic cutoff after model-based scoring.
    return [
        chunk
        for score, chunk in sorted(scored_chunks, reverse=True)
        if score >= 0.6
    ][:max_chunks]
```

## Risks

- reranker latency;
- model cost;
- loss of recall from aggressive cutoff;
- compression removing qualifying language;
- summary hallucination.

## Rule

Rerank candidates; do not ask the strongest model to search the entire corpus.
