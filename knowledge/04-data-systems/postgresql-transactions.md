# PostgreSQL & Transaction Design

## 1. Database design starts from invariants

A schema should preserve business rules, not merely mirror frontend forms.

Examples:

- a claim belongs to exactly one tenant;
- approved claims cannot be edited;
- payment IDs are unique;
- balances must not become negative.

Some invariants belong in application logic; others are safer as database constraints.

## 2. Transactions

A transaction groups changes into one atomic unit.

The application should choose transaction boundaries around business invariants.

```python
async with session.begin():
    claim = await repo.get_for_update(claim_id)
    claim.approve(actor_id)
    await repo.save(claim)
    await outbox.add("ClaimApproved", claim.id)
```

The business change and outbox event are committed together.

## 3. Isolation

Important anomalies include:

- dirty read;
- non-repeatable read;
- phantom read;
- lost update;
- write skew.

Higher isolation can reduce anomalies but increase contention and retries.

## 4. Indexes

Indexes trade write/storage cost for read speed.

Index based on real query patterns:

- filter columns;
- join keys;
- sort keys;
- uniqueness constraints;
- composite access patterns.

Use `EXPLAIN ANALYZE` instead of assuming an index helps.

## 5. Locking

Pessimistic locking is useful when conflicting writes must be serialized.

Optimistic concurrency uses a version field or compare-and-swap style update.

## 6. Connection pooling

A database cannot accept unlimited connections.

Pool size should consider:

- service replicas;
- DB capacity;
- transaction duration;
- query latency;
- burst behavior.

## 7. Production concerns

- migration safety;
- backup/restore;
- replication;
- failover;
- query latency;
- vacuum/autovacuum;
- long transactions;
- connection exhaustion;
- slow-query telemetry.

## 8. Decision rule

Use PostgreSQL as the default when relational integrity, transactions, and rich querying matter. Add specialized stores only when a measurable access-pattern need justifies them.
