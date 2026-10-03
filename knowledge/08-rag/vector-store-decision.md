# Vector Store Decision Framework

## Dimensions

Evaluate:

- vector scale;
- lexical search;
- hybrid retrieval;
- metadata filtering;
- tenancy;
- update/freshness behavior;
- operations;
- latency;
- cost;
- cloud coupling;
- backup/recovery;
- ecosystem.

## pgvector

Good when PostgreSQL already exists and vector scale/latency requirements fit.

Benefits:

- one operational database;
- relational joins/metadata;
- transactions.

Trade-offs:

- not always ideal for very large specialized vector workloads;
- index tuning matters.

## OpenSearch

Good when:

- BM25 + vectors are both important;
- full search capabilities matter;
- filters/aggregations matter.

Trade-off: heavier cluster operations.

## Pinecone

Managed vector-first option when low operational burden matters.

Evaluate feature fit and cost.

## Qdrant

Vector-first engine with strong filtering and self-host/managed options.

## Chroma

Useful for:

- learning;
- notebooks;
- local prototypes;
- smaller applications.

## Decision rule

Do not ask "Which vector database is best?"

Ask:

> Which retrieval engine satisfies my search modes, filtering, scale, operations, and cost constraints with the least unnecessary complexity?
