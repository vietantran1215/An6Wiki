# Agent Evaluation

## What to measure

- task success;
- tool-selection accuracy;
- argument correctness;
- policy compliance;
- step count;
- recovery success;
- escalation rate;
- latency;
- cost.

## Trajectory evaluation

For agents, the final answer can be correct even when the path is unsafe or unnecessarily expensive.

Evaluate the trajectory:

```text
state
 → action
 → tool
 → observation
 → next action
```

## Example rule-based evaluator

```python
def evaluate_trajectory(trace):
    violations = []

    if trace.tool_calls > 10:
        violations.append("tool-budget-exceeded")

    if any(call.name == "delete_claim" for call in trace.calls) and not trace.human_approved:
        violations.append("approval-missing")

    return violations
```

## Counterfactual cases

Test:

- tool fails;
- retrieval empty;
- user lacks permission;
- model proposes forbidden action;
- human rejects approval;
- state resumes after restart.

## Rule

Agent quality is task success under policy and resource constraints—not task success at any cost.
