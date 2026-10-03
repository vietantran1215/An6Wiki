# Harness Architecture

## Why harness engineering exists

A production AI system needs deterministic infrastructure around probabilistic models.

Reference architecture:

```text
User / Event
   ↓
Identity + Gateway
   ↓
Policy / Risk
   ↓
Orchestrator / Runtime
   ├── Context Engine / RAG
   ├── Memory / State
   ├── Model Router
   ├── Tool Registry / MCP
   ├── Verifier
   └── Human Approval
   ↓
Audit + Observability + Evaluation
```

## Five useful layers

### Context

What information is available?

### Tools

What capabilities exist?

### Sensors

What observations/events update state?

### Operations

What bounded action can be performed?

### Orchestration

How are branches, retries, approvals, checkpoints, and termination controlled?

## Cross-cutting control plane

The harness also owns:

- identity;
- policy;
- budgets;
- model routing;
- versioning;
- audit;
- eval gates;
- telemetry.

## Example policy wrapper

```python
def invoke_tool(call, principal, budget):
    if budget.tool_calls_remaining <= 0:
        raise RuntimeError("Tool budget exhausted")

    decision = policy.authorize(principal, call)

    if not decision.allowed:
        raise PermissionError(decision.reason)

    if decision.requires_approval:
        return pause_for_human(call)

    return tool_registry.invoke(call)
```

## Rule

A harness is justified when many workflows need the same reliable control primitives. It should reduce duplicated safety/operations logic across agents.
