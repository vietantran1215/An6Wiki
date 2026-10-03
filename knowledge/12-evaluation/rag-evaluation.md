# RAG Evaluation

## Component view

```text
query
 → retrieval
 → reranking
 → context
 → generation
```

Evaluate each component.

## Retrieval metrics

- Recall@K;
- Precision@K;
- MRR;
- nDCG.

## Generation metrics

Common dimensions:

- faithfulness;
- answer relevance;
- completeness;
- citation correctness.

Frameworks such as RAGAS can help automate parts of evaluation, but metric validity still depends on dataset design and evaluator quality.

## Retrieval example

```python
def recall_at_k(retrieved: list[str], relevant: set[str], k: int) -> float:
    if not relevant:
        return 1.0

    hits = len(set(retrieved[:k]) & relevant)
    return hits / len(relevant)
```

## Permission metric

Security-sensitive RAG should explicitly test leakage:

```text
unauthorized_retrieval_rate = unauthorized_hits / protected_queries
```

Target should be zero for access-control violations.

## Rule

If the final answer is wrong, component metrics should help locate whether retrieval, context, or generation caused the failure.
