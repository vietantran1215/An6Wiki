# Durable Execution, Recovery & Governance

## Durable execution

A long-running workflow should survive:

- process restart;
- deployment;
- dependency outage;
- human waiting period.

Store durable state/checkpoints outside process memory.

## Idempotent step design

Every resumable step should consider duplicate execution.

Use:

- idempotency key;
- version check;
- inbox/outbox;
- compare-and-swap;
- durable step status.

## Recovery categories

- retry transient failure;
- fallback to alternate provider/tool;
- wait for dependency;
- compensate completed action;
- escalate to human;
- terminate safely.

## Example step state

```json
{
  "workflowId": "wf_123",
  "step": "approve-payment",
  "attempt": 2,
  "status": "waiting_for_human",
  "checkpointVersion": 7
}
```

## Governance

Record:

- workflow version;
- prompt/model/tool versions;
- principal;
- policy decisions;
- state transitions;
- approvals;
- tool side effects.

## Rule

If an agent can perform business actions, recovery and auditability are as important as reasoning quality.
