# LangChain, LangGraph & LangSmith

## LangChain

Use LangChain primarily for reusable LLM application abstractions:

- model interfaces;
- tools;
- structured output;
- retrieval components;
- agent helpers.

Avoid deeply nested abstractions when explicit code would be clearer.

## LangGraph

Use LangGraph when workflow state and transitions are first-class:

- loops;
- conditional routing;
- checkpoints;
- human interrupts;
- subgraphs;
- long-running execution.

## LangSmith

Use LangSmith for:

- traces;
- datasets;
- evaluations;
- experiments;
- prompt/model comparison.

## Architecture split

```text
LangChain components
        ↓
LangGraph orchestration
        ↓
Application services / tools
        ↓
LangSmith traces + evaluation
```

## Example node

```python
def retrieve_node(state):
    docs = retriever.invoke(state["query"])
    return {"documents": docs}
```

Keep nodes small and observable.

## Rule

Frameworks should make state, contracts, and telemetry clearer. If the abstraction hides execution flow, reduce the abstraction.
