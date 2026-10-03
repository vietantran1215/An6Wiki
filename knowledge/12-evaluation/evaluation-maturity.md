# Evaluation Maturity & Release Gates

## Level 0 — Eyeball

Manual testing.

Useful for exploration, not regression.

## Level 1 — End-to-end dataset

Score final answers against a golden set.

## Level 2 — Component evaluation

Evaluate retrieval, reranking, context, generation, and tools independently.

## Level 3 — Regression gates

Run eval automatically when changing:

- model;
- prompt;
- chunking;
- embedding;
- retriever;
- reranker;
- tool;
- policy.

## Level 4 — Online production evaluation

Monitor:

- user feedback;
- fallback rate;
- no-answer rate;
- latency;
- cost;
- safety violations;
- tool failures.

## Level 5 — Enterprise evaluation system

Add:

- ownership;
- versioning;
- approvals;
- audit;
- risk-tier thresholds;
- drift review;
- incident feedback.

## Release gate example

```python
def release_allowed(report):
    return (
        report.retrieval_recall >= 0.90
        and report.faithfulness >= 0.95
        and report.permission_leaks == 0
        and report.critical_failures == 0
    )
```

## Rule

Evaluation becomes engineering when it is repeatable, versioned, automated, and tied to release decisions.
