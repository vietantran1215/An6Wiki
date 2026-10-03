# Human-in-the-Loop & Oversight

## Why human approval exists

HITL is useful when:

- impact is high;
- policy requires accountability;
- model uncertainty is material;
- action is irreversible;
- context is insufficient.

## Approval should be contextual

A useful approval request shows:

- proposed action;
- reason;
- evidence;
- affected resource;
- risk;
- side effects.

Do not ask a human to approve an opaque "agent wants to continue."

## Risk-based gate

```python
def approval_required(action) -> bool:
    return (
        action.is_irreversible
        or action.financial_impact > 1000
        or action.risk_level == "high"
    )
```

## Human response

Support:

- approve;
- reject;
- edit;
- ask for more evidence.

## Checkpointing

The workflow must persist before waiting for a person.

Otherwise process restart can lose the pending decision.

## Audit

Record:

- proposed action;
- model/tool version;
- approver;
- decision;
- timestamp;
- final executed action.

## Rule

HITL is not a substitute for weak policy. Use humans where judgment/accountability is genuinely required.
