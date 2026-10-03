# Agentic AI & LangGraph

## 1. What makes a system agentic?

An agent selects actions based on state and feedback. Typical capabilities include routing/planning, tools, retrieval, memory/state, iterative correction, verification, termination rules, and human approval.

## 2. Agentic RAG

Agentic RAG dynamically decides whether retrieval is needed, which retrieval/tool path to use, whether to rewrite/decompose a query, whether evidence is sufficient, and whether another loop is justified.

```text
Naive RAG
 → Advanced RAG
 → Corrective / Adaptive RAG
 → Agentic RAG
 → Multi-agent RAG when specialization is justified
```

Agentic does not imply multi-agent.

## 3. LangGraph mental model

LangGraph provides state, nodes, edges, conditional edges, checkpoints, interrupts, and explicit loops.

```python
from typing import TypedDict

class AgentState(TypedDict):
    question: str
    documents: list[str]
    retries: int

def should_retry(state: AgentState) -> str:
    # Explicit control prevents unbounded loops.
    if state["documents"]:
        return "generate"
    if state["retries"] >= 2:
        return "fallback"
    return "rewrite"
```

## 4. Bounded autonomy

Every loop should have a retry limit, time budget, token/cost budget, tool allowlist, termination condition, and fallback.

## 5. Multi-agent rule

Use multiple agents when responsibilities, permissions, context scopes, tools, evaluation criteria, or ownership boundaries genuinely differ.

## 6. Human-in-the-loop

Require approval before consequential actions such as destructive data changes, external communication, financial operations, high-risk production changes, and irreversible workflow transitions.

## 7. Trust boundaries

Separate Planner, Verifier, and Executor. The model may propose an action; deterministic policy should decide whether execution is allowed.
