# 01 — Software Engineering Foundations

## Scope

This section establishes the substrate required before discussing architecture, distributed systems, or AI systems.

Study in this order:

1. Runtime and execution model.
2. HTTP and API semantics.
3. State and persistence.
4. Concurrency and asynchronous I/O.
5. Failure and resilience.
6. Testing and observability.
7. Security boundaries.

## Core chapters

- [Runtime, Concurrency & Async I/O](./runtime-concurrency-async.md)
- [HTTP, APIs & Contracts](./http-api-contracts.md)
- [Resilience Patterns](./resilience-patterns.md)

## Capability target

You should be able to explain not only what code does, but:

- where it runs;
- what it blocks;
- how state changes;
- what can fail;
- how failure propagates;
- how retries affect correctness;
- how the system is observed;
- how an external caller can safely depend on the contract.
