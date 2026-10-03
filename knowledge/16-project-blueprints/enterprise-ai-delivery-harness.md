# Enterprise AI Delivery Harness

## Goal

Build a reusable enterprise runtime for project-aware AI delivery.

## Core use case

An AI system can understand project knowledge, plan engineering work, propose actions, and execute approved Jira/GitHub-style operations while preserving policy, audit, evaluation, and recovery.

## Reference architecture

```text
User
 ↓
Identity / Tenant / Project Scope
 ↓
Harness Runtime
 ├─ Knowledge Plane
 │    └─ permission-aware hybrid RAG
 ├─ Planner
 ├─ Risk / Policy Engine
 ├─ Tool Gateway
 ├─ Verifier
 ├─ Human Approval
 └─ Durable State
 ↓
Git / Issue / Delivery Systems

Cross-cutting:
evaluation + observability + audit + security
```

## Progressive sequence

### 1. Harness skeleton

- typed state;
- workflow graph;
- model gateway;
- tool registry;
- traces.

### 2. Knowledge plane

- document ingestion;
- project/tenant ACL;
- hybrid retrieval;
- reranking;
- citations.

### 3. Agent orchestration

- planner;
- verifier;
- retry/fallback;
- termination budgets.

### 4. Tool gateway

- typed tools;
- dry run;
- idempotency;
- human approval;
- audit.

### 5. Evaluation gates

- golden tasks;
- retrieval metrics;
- tool correctness;
- critical-risk gates.

### 6. Security

- prompt injection;
- data leakage;
- least privilege;
- tool abuse;
- red-team cases.

### 7. Reliability

- durable checkpoints;
- queues;
- recovery;
- circuit breakers;
- model/provider fallback.

### 8. Architecture defense

The final deliverable must include:

- Architecture Spec;
- Test Spec;
- working code;
- evaluation report;
- runbook;
- threat model;
- technical defense.

## Rule

The capstone is successful only when the system can explain, constrain, observe, and recover from its own AI-driven execution.
