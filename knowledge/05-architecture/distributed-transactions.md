# Distributed Transactions, Outbox & Saga

## 1. The problem

A local ACID transaction cannot atomically include another service or broker without additional coordination.

Example:

```text
update payment DB
publish PaymentCompleted event
```

If the DB commit succeeds but publish fails, state diverges.

## 2. Transactional outbox

Write the domain change and event record in the same transaction.

```text
BEGIN
  update payment
  insert outbox event
COMMIT

publisher:
  read outbox
  publish
  mark sent
```

Duplicates can still occur, so consumers should be idempotent.

## 3. Saga

A saga coordinates multiple local transactions.

Two broad styles:

- choreography — services react to events;
- orchestration — a coordinator drives steps.

## 4. Compensation

Distributed rollback often means compensating action, not database rollback.

Example:

```text
reserve inventory
charge payment
shipping fails
 → refund payment
 → release inventory
```

Compensation itself can fail and needs retry/operations.

## 5. Decision rule

Use local transactions whenever possible.

Use outbox for reliable event publication.

Use saga when a business workflow spans multiple independently owned transactional boundaries.
