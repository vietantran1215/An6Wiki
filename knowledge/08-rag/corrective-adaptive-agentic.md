# Corrective, Adaptive & Agentic RAG

## Corrective RAG

Evaluate retrieved evidence before generation.

```text
retrieve
 → grade evidence
 ├─ sufficient → answer
 └─ weak → rewrite / alternate retrieval / web
```

## Adaptive RAG

Route based on query type or complexity.

```text
query
 ├─ exact lookup → BM25
 ├─ semantic → hybrid
 ├─ structured → SQL
 ├─ relationship → graph
 └─ no retrieval → direct
```

## Agentic RAG

The runtime chooses the next action based on state.

Actions may include:

- retrieve;
- rewrite;
- decompose;
- use tool;
- verify;
- stop.

## Bounded loop

```python
MAX_STEPS = 6

for step in range(MAX_STEPS):
    decision = choose_next_action(state)

    if decision.type == "finish":
        break

    state = execute(decision, state)
else:
    state = fallback(state)
```

## When to escalate

Move from baseline to corrective/adaptive/agentic only when evaluation shows a failure pattern the additional mechanism can address.

## Rule

Complex retrieval control is justified by heterogeneous queries and measurable failures, not by the word "agentic."
