# Software Engineering Foundations

## 1. What makes software engineering different from coding?

Coding produces implementation. Software engineering produces a system that can be changed, tested, operated, understood, and trusted over time.

The recurring engineering dimensions are:

- correctness;
- maintainability;
- modularity;
- testability;
- observability;
- reliability;
- performance;
- security;
- cost;
- operability.

## 2. Core foundations

### HTTP and APIs

Understand methods, status codes, headers, cookies, caching, idempotency, authentication, authorization, timeouts, and retries.

### Data

Learn SQL before hiding it behind an ORM. Understand:

- schema design;
- indexes;
- transactions;
- isolation;
- query plans;
- consistency;
- migrations;
- data ownership.

### Concurrency

Know the difference between:

- concurrency and parallelism;
- blocking and non-blocking work;
- bounded and unbounded concurrency;
- backpressure and overload.

### Failure handling

Production systems must expect failure.

Key patterns:

- timeout;
- retry with exponential backoff and jitter;
- circuit breaker;
- bulkhead;
- rate limiting;
- idempotency;
- dead-letter queue;
- graceful degradation;
- graceful shutdown.

## 3. A preferred learning progression

1. Language and runtime.
2. HTTP and API design.
3. SQL and persistence.
4. Testing.
5. Modular application architecture.
6. Caching and queues.
7. Deployment and CI/CD.
8. Observability.
9. Distributed-system failure modes.
10. Security and governance.

## 4. Design rule

Do not jump from a small CRUD application directly to microservices.

A better progression is:

```text
Modular monolith
    ↓
Event-driven modules
    ↓
Distributed components where justified
    ↓
Microservices only when independent ownership/scaling/change justify them
```

## 5. Engineering evidence

A strong implementation should be able to answer:

- What problem does this solve?
- What assumptions does it make?
- What happens when a dependency is slow or unavailable?
- How is the behavior tested?
- How is it observed?
- How is it rolled back?
- What are the security boundaries?
