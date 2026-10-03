# Agent Runtime Fundamentals

## 1. What makes an application agentic?

A model call becomes agentic when the system can select among actions based on current state and observations.

Typical actions:

- retrieve;
- call a tool;
- inspect a result;
- rewrite;
- ask for approval;
- retry;
- terminate.

## 2. Core loop

```text
state
 → decide action
 → execute
 → observe result
 → update state
 → continue or stop
```

## 3. Deterministic shell

The LLM should not own:

- authorization;
- irreversible action policy;
- step limits;
- cost budget;
- retry limits;
- secret access.

These belong to deterministic runtime logic.

## 4. Example bounded loop

```python
MAX_STEPS = 8

def run_agent(state):
    for _ in range(MAX_STEPS):
        action = planner.next_action(state)

        if action.kind == "finish":
            return action.output

        if not policy.allows(action, state.principal):
            return {"status": "denied"}

        observation = executor.execute(action)
        state = state.apply(observation)

    return {"status": "fallback", "reason": "step_budget_exhausted"}
```

## 5. Budgets

A production agent should have:

- step budget;
- time budget;
- token budget;
- tool-call budget;
- cost budget;
- retry budget.

## 6. Failure modes

- infinite loops;
- repeated tool calls;
- hallucinated arguments;
- tool timeout;
- inconsistent state;
- unsafe action selection;
- silent partial completion.

## 7. Rule

Agent intelligence should be elastic. Runtime constraints should be explicit and deterministic.
