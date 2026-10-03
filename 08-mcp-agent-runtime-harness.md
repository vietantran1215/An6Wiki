# MCP, Agent Runtime & Harness Engineering

## 1. MCP is not an agent runtime

MCP standardizes exposure of tools, resources, and prompts. It does not automatically provide business authorization, durable execution, retries, orchestration, memory, approval, audit, evaluation, or recovery.

## 2. Production harness

```text
User / Event
   ↓
Gateway + Identity
   ↓
Policy / Risk Classifier
   ↓
Orchestrator / Runtime
   ├── Context / RAG
   ├── Memory / State
   ├── Model Router
   ├── Tool Registry / MCP
   ├── Verifier
   └── Human Approval
   ↓
Audit + Observability + Evaluation
```

## 3. Harness responsibilities

Orchestration, durable state, checkpoints, context engineering, memory, tools, permissions, retries/timeouts, fallbacks, policies, model routing, observability, evaluation, human oversight, and security.

## 4. Layered model

- Context layer — what information is available?
- Tool layer — what capabilities exist?
- Sensor layer — what observations/events update state?
- Operation layer — what bounded action is performed?
- Orchestration layer — how are branches, retries, approvals, and termination managed?

## 5. MCP security

Treat each MCP tool as a privileged API. Require strict schemas, identity, authorization, validation, timeouts, rate limits, sandboxing where appropriate, and audit logs.

## 6. Why harness engineering matters

The runtime must control what the model can see, call, change, how long it can loop, how errors recover, what requires approval, and how behavior is evaluated.
