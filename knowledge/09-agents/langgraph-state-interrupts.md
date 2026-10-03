# LangGraph: State, Nodes, Checkpoints & Interrupts

## 1. Mental model

LangGraph models the workflow as a graph over shared state.

Concepts:

- state;
- node;
- edge;
- conditional edge;
- checkpoint;
- interrupt;
- subgraph.

## 2. State

State should contain information required to continue execution.

```python
from typing import TypedDict

class ClaimAgentState(TypedDict):
    claim_id: str
    principal_id: str
    evidence: list[str]
    risk_level: str | None
    retries: int
    approved: bool
```

Avoid stuffing every raw artifact into state. Store references for large payloads.

## 3. Nodes

Each node should do one bounded piece of work.

Examples:

- classify request;
- retrieve policy;
- assess risk;
- request human approval;
- execute action.

## 4. Conditional routing

```python
def route_after_risk(state: ClaimAgentState) -> str:
    if state["risk_level"] == "high":
        return "human_approval"

    return "execute"
```

## 5. Checkpointing

Checkpointing allows workflows to:

- resume after interruption;
- survive process restarts;
- wait for human input;
- audit state transitions.

## 6. Interrupts

An interrupt pauses the graph before a consequential step.

Use for:

- production changes;
- deletion;
- external messaging;
- payment;
- high-risk policy decision.

## 7. Streaming

LangGraph streaming can expose:

- state updates;
- node progress;
- model tokens;
- custom events.

Useful for observability and interactive UX.

## 8. Rule

Model a workflow graph when state transitions matter. Do not use a graph merely to turn a linear function into more files.
