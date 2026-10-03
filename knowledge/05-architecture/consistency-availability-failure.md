# Consistency, Availability & Failure

## 1. Partial failure

In distributed systems, one component can fail while others continue.

This creates ambiguity:

- Did the request arrive?
- Was it committed?
- Was the response lost?
- Should the caller retry?

## 2. Consistency

Strong consistency makes reads reflect the latest committed write under the defined model.

Eventual consistency allows temporary divergence.

Choose based on business invariant, not architectural fashion.

## 3. Example

A social feed can often tolerate eventual consistency.

A financial balance check before spending may require stronger guarantees.

## 4. CAP nuance

CAP concerns behavior during network partition:

- consistency;
- availability;
- partition tolerance.

Real systems also trade:

- latency;
- freshness;
- operational complexity;
- cost.

## 5. Failure containment

Use:

- timeouts;
- bulkheads;
- circuit breakers;
- queue isolation;
- per-tenant quotas;
- load shedding.

## 6. Recovery

Architecture is incomplete without recovery design:

- replay events;
- rebuild read models;
- restore backups;
- reprocess DLQ;
- reconcile inconsistent state.

## 7. Rule

Every distributed write path should answer: "What if the caller cannot know whether the operation succeeded?"
