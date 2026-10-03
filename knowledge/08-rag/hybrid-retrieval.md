# Lexical, Dense & Hybrid Retrieval

## BM25

BM25 excels when exact terms matter:

- identifiers;
- error messages;
- product codes;
- names;
- code symbols.

## Dense retrieval

Dense embeddings excel when semantic similarity matters even if exact wording differs.

## Hybrid retrieval

Use both when the corpus contains both lexical and semantic signals.

```text
query
 ├─ BM25 search
 └─ dense search
       ↓
    rank fusion
       ↓
    reranker
```

## Reciprocal Rank Fusion

```python
from collections import defaultdict

def rrf(*rankings: list[str], k: int = 60) -> list[str]:
    scores = defaultdict(float)

    for ranking in rankings:
        for rank, doc_id in enumerate(ranking, 1):
            scores[doc_id] += 1.0 / (k + rank)

    return sorted(scores, key=scores.get, reverse=True)
```

RRF avoids requiring BM25 and vector scores to share the same scale.

## Metadata filtering

Use metadata for:

- tenant;
- ACL;
- document type;
- date;
- project;
- source version.

Authorization filters must come from trusted identity context.

## Retrieval evaluation

Measure:

- Recall@K;
- Precision@K;
- MRR;
- nDCG;
- zero-result rate;
- latency.

## Rule

The first retrieval stage should prioritize candidate recall. Use reranking to improve precision afterward.
