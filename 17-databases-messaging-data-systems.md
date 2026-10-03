# Databases, Messaging & Data Systems

## Relational databases

Core topics:

- schema design;
- normalization and denormalization;
- indexes;
- transactions;
- isolation;
- query plans;
- migrations;
- locking;
- connection pooling.

PostgreSQL is a strong default for transactional systems and can also support full-text and vector workloads.

## NoSQL

Document databases such as MongoDB are useful when document-shaped access patterns dominate. Choose them because of data and query characteristics, not because "schema-less" sounds simpler.

## Redis

Common uses:

- cache;
- rate limiting;
- short-lived state;
- distributed coordination;
- queues/streams in some systems.

Caching requires explicit invalidation and TTL strategy.

## RabbitMQ vs Kafka

RabbitMQ commonly fits task/message routing and work queues.

Kafka commonly fits durable event streams, replay, high throughput, and event-log architectures.

## Delivery semantics

Understand:

- at-most-once;
- at-least-once;
- duplicate delivery;
- ordering scope;
- consumer acknowledgements/offsets;
- idempotent consumers.

"Exactly once" business behavior usually comes from infrastructure guarantees plus application-level idempotency.

## Data ownership

Each service should own its authoritative data. Cross-service read models should be deliberate, versioned, and observable.
