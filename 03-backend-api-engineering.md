# Backend & API Engineering

## 1. What should a backend service own?

A backend service should have an explicit boundary and own its business rules, data model, invariants, and external contracts.

Recurring stacks include Node.js/TypeScript/Express/NestJS, Python/FastAPI/Django, PostgreSQL/MySQL/MongoDB, Redis, RabbitMQ, and Kafka.

## 2. API design

A strong API defines resource model, schemas, validation, authentication, authorization, error contract, idempotency, pagination, rate limits, and versioning strategy.

## 3. Authentication vs authorization

Authentication answers: **Who are you?**

Authorization answers: **What are you allowed to do with this resource in this state?**

Production authorization can combine RBAC with resource ownership, tenant boundary, workflow state, and policy rules.

## 4. Transactional boundaries

For reliable cross-service event delivery, use a transactional outbox:

```text
DB transaction:
  update business state
  insert outbox event
commit

Background publisher:
  read unsent outbox rows
  publish message
  mark as sent
```

## 5. Idempotency

```ts
const processed = new Set<string>();

export async function handleRequest(requestId: string) {
  if (processed.has(requestId)) {
    return { status: "already-processed" };
  }

  // Perform the business operation.
  processed.add(requestId);
  return { status: "processed" };
}
```

Use durable storage in real systems.

## 6. Async/event-driven systems

Understand delivery semantics, ordering, duplicate messages, idempotent consumers, retries, DLQs, backpressure, eventual consistency, sagas, and schema evolution.

## 7. Boundary rule

A service should not directly read another service's private database merely because it is convenient. Use a contract: API, event, or deliberately designed shared data product.
