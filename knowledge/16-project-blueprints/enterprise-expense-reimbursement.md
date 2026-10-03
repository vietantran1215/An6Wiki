# Enterprise Expense Reimbursement Platform

## Goal

Build one coherent enterprise domain and progressively evolve it from a small FastAPI service into a secure AI-enabled platform.

The domain remains stable so each phase teaches architecture rather than introducing unrelated business problems.

## Service model

```text
Auth Service
  owns identity, credentials, sessions, tokens

Core Service
  owns claims, claim items, receipts, workflow

AI Service
  owns RAG, evaluation, routing, agents

MCP Server
  exposes approved Core capabilities to agents
```

## Phase 1 — Core API

Teach:

- FastAPI;
- Pydantic;
- SQLAlchemy;
- Alembic;
- PostgreSQL;
- validation;
- testing;
- error contracts.

Keep business scope deliberately small.

## Phase 2 — Production Auth

Deepen:

- password security;
- JWT/access tokens;
- refresh rotation;
- revocation;
- sessions/devices;
- rate limiting;
- lockout;
- audit;
- RBAC + resource/attribute rules.

## Phase 3 — Basic RAG

Use policy/manual documents.

Pipeline:

```text
ingestion → chunking → embeddings/index
 → retrieval → context → answer + citations
```

## Phase 4 — Evaluation & Observability

Add:

- golden dataset;
- RAGAS-style metrics;
- traces;
- latency;
- tokens;
- cost;
- regression suite.

## Phase 5 — Agentic RAG

The agent can:

- retrieve policy;
- inspect claim;
- reason about missing evidence;
- request additional context.

Do not allow unrestricted writes yet.

## Phase 6 — Adaptive + Hybrid + Reranking

Route queries among:

- BM25;
- dense;
- hybrid;
- SQL/tool lookup.

Add reranking and measured comparison.

## Phase 7 — Multimodal RAG

Receipts introduce:

- OCR;
- image evidence;
- layout/table extraction;
- receipt-to-claim linkage.

## Phase 8 — MCP

Expose bounded Core tools:

- get_claim;
- list_claim_items;
- submit_claim;
- get_policy_context.

Propagate identity and authorization.

## Phase 9 — LLM Security

Harden:

- permission-aware retrieval;
- prompt injection;
- sensitive-data handling;
- provenance;
- output validation.

## Phase 10 — Agentic Security

Add:

- tool risk classification;
- human approval;
- cost/step budgets;
- audit;
- recovery;
- kill switch.

## Why this blueprint works

Each phase adds one new architectural dimension while keeping the business model familiar.
