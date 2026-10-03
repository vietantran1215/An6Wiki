# Multi-Agent Design

## 1. When multiple agents are justified

Use multiple agents when there are meaningful differences in:

- responsibility;
- permission;
- context;
- tool set;
- evaluation;
- ownership.

## 2. Good specialization

Example:

```text
Planner Agent
  proposes execution plan

Security Verifier
  evaluates policy/risk

Domain Agent
  handles business reasoning

Executor
  performs approved tool calls
```

These roles have different trust boundaries.

## 3. Weak specialization

Creating "research agent", "thinking agent", "smart agent", and "manager agent" without distinct contracts usually adds coordination overhead without real capability gain.

## 4. Communication

Agent-to-agent messages should use typed contracts.

```python
class ReviewRequest(BaseModel):
    task_id: str
    artifact_ref: str
    required_checks: list[str]
```

## 5. Shared state

Avoid uncontrolled shared mutable memory.

Prefer:

- explicit handoff;
- durable task state;
- artifact references;
- typed messages.

## 6. Evaluation

Evaluate both:

- individual agent performance;
- system-level coordination.

Metrics:

- handoff accuracy;
- duplicated work;
- tool-call count;
- latency;
- cost;
- escalation rate.

## 7. Rule

Multi-agent architecture should encode real separation of responsibility, not simulate organizational charts for aesthetics.
