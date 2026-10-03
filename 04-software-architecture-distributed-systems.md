# Software Architecture & Distributed Systems

## 1. What is architecture?

Architecture is the set of high-impact decisions that shape a system's qualities, boundaries, dependencies, and evolution.

Start from architecture-significant requirements:

- availability;
- scalability;
- latency;
- consistency;
- security;
- maintainability;
- deployability;
- recoverability;
- cost.

## 2. Architecture progression

```text
Single application
    ↓
Modular monolith
    ↓
Event-driven modules
    ↓
Distributed services
    ↓
Microservices where independent scaling/ownership is valuable
```

## 3. Distributed-system topics

- replication;
- partitioning;
- consistency;
- consensus;
- leader election;
- distributed transactions;
- eventual consistency;
- messaging semantics;
- partial failure;
- backpressure.

## 4. Architectural styles

### Modular monolith

Prefer when one deployment is acceptable and strong internal boundaries are sufficient.

### Microservices

Use when independent scaling, ownership, deployment, fault isolation, or change cadence justify operational complexity.

### Event-driven architecture

Useful for decoupling and asynchronous workflows. It introduces ordering, duplicate delivery, schema evolution, replay, and observability concerns.

## 5. ADR

Capture Context, Decision, Alternatives, Trade-offs, Consequences, and Revisit Condition.

## 6. Reliable integration patterns

Transactional Outbox, Idempotent Consumer, Saga/Process Manager, Retry with Jitter, Circuit Breaker, DLQ, and Expand → Migrate → Contract.

## 7. Architecture review questions

- What are the failure domains?
- Which dependencies are synchronous?
- Where can backpressure propagate?
- What state is authoritative?
- Which operations require strong consistency?
- Can duplicate delivery be tolerated?
- What is the rollback path?
- What is measured in production?
