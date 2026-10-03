# Projects, Capstones & Case Studies

## 1. Why projects matter

Projects should integrate capabilities under realistic constraints rather than become feature dumps.

A good capstone has one coherent domain, progressive architecture, reproducible setup, explicit non-goals, measurable quality, and production trade-offs.

## 2. Canonical project: Enterprise Expense Reimbursement

Ten-stage progression:

1. Core API with strong fundamentals.
2. Deep authentication/authorization service.
3. Basic RAG service.
4. RAG evaluation and observability.
5. Agentic RAG.
6. Adaptive routing, hybrid retrieval, reranking.
7. Multimodal RAG for receipts/PDFs.
8. MCP server over controlled Core capabilities.
9. OWASP LLM application security hardening.
10. OWASP agentic-application security hardening.

### Service boundaries

```text
Auth Service
  owns identity, credentials, tokens, sessions

Core Service
  owns claims, items, receipts, workflow state

AI Service
  owns retrieval, models, RAG, agents, evaluation

MCP Server
  bounded adapter over approved Core capabilities
```

The AI service should not bypass Core APIs to read the Core database directly.

## 3. AI-assessment project pattern

Use repository snapshots, AST/code-aware indexing, cross-repository dependency graphs, hybrid retrieval, graph traversal, adaptive questions, deterministic grading, evidence-linked answers, trainer/admin UI, telemetry, and evaluation.

## 4. Review questions

Is the domain coherent? Does each phase introduce a justified capability? Is every phase runnable? Are dependencies minimal? Can quality be measured? Are trust boundaries explicit? Can the system fail safely?
