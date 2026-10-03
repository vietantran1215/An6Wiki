# Harness Engineering Decision Framework

## When a simple LLM application is enough

Use a simple request/response application when:

- one model call is sufficient;
- no durable workflow exists;
- no privileged action is executed;
- failure recovery is simple;
- context is small and predictable.

## When to add a workflow graph

Add orchestration when the system needs:

- branching;
- retries;
- explicit state;
- multiple retrieval/tool stages;
- checkpoints;
- human approval.

## When to add an agent

Use an agent when action selection cannot be fully predetermined and the system benefits from controlled dynamic choice.

The runtime still requires deterministic limits.

## When to add multiple agents

Use multiple agents only when there are meaningful differences in:

- responsibility;
- permissions;
- tool access;
- context scope;
- evaluation;
- ownership.

## When a harness becomes necessary

A production harness is justified when the AI system has multiple cross-cutting control requirements:

- identity;
- policy;
- durable state;
- tool registry;
- MCP integration;
- memory;
- context engineering;
- model routing;
- evaluation;
- observability;
- cost controls;
- human approval;
- incident recovery.

## Runtime responsibilities

```text
Identity
  ↓
Policy
  ↓
Orchestrator
  ├─ state/checkpoints
  ├─ context/RAG
  ├─ model routing
  ├─ tools/MCP
  ├─ verifier
  └─ HITL
  ↓
Audit + telemetry + evaluation
```

## Anti-pattern

Do not use "multi-agent" as a synonym for "advanced".

More agents increase:

- coordination cost;
- latency;
- debugging difficulty;
- token cost;
- failure surface;
- permission complexity.

Start with the smallest architecture that satisfies the workflow and its reliability requirements.
