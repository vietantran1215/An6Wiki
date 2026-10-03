# Schema Evolution & Data Ownership

## 1. Data ownership

A service owns data when it controls:

- schema;
- writes;
- invariants;
- lifecycle;
- authoritative interpretation.

Other services should not bypass that boundary and directly mutate its database.

## 2. Why shared databases become dangerous

Shared tables create:

- hidden coupling;
- release coordination;
- unclear ownership;
- bypassed invariants;
- difficult migrations.

## 3. Expand → migrate → contract

A safe migration pattern:

1. Add new schema without breaking old readers.
2. Deploy code that supports both representations.
3. Migrate/backfill data.
4. Verify.
5. Switch traffic.
6. Remove the old representation later.

## 4. Example

Suppose `full_name` becomes `first_name` + `last_name`.

Do not rename/drop in one deployment.

Instead:

- add new columns;
- dual-read or dual-write temporarily;
- backfill;
- update consumers;
- verify;
- remove `full_name`.

## 5. Event schema evolution

For events:

- prefer additive fields;
- keep old consumers compatible;
- version truly breaking contracts;
- document semantics, not only JSON shape.

## 6. Decision rule

Treat schema change as a distributed rollout problem whenever more than one independently deployed component depends on the data.
