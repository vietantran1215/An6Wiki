# An6Wiki v2 — Canonical Knowledge Base

This directory is the canonical, long-form knowledge layer of An6Wiki.

The root-level files remain useful as compressed summaries. Files under `knowledge/` are designed for serious learning, architecture work, production decisions, training, and interview preparation.

## Knowledge model

Every substantial topic should answer seven questions:

1. **What is it?** — first principles and vocabulary.
2. **How does it work?** — mechanics and execution model.
3. **How do I implement it?** — concrete code or configuration.
4. **What changes in production?** — reliability, security, observability, cost, and operations.
5. **How does it fail?** — failure modes and debugging.
6. **What are the trade-offs?** — what is gained and lost.
7. **When should I choose it?** — decision rules.

## Domain map

- [01 — Software Foundations](./01-foundations/README.md)
- [02 — Frontend Engineering](./02-frontend/README.md)
- [03 — Backend & API Engineering](./03-backend/README.md)
- [04 — Databases, Caching & Messaging](./04-data-systems/README.md)
- [05 — Architecture & Distributed Systems](./05-architecture/README.md)
- [06 — Cloud, DevOps & SRE](./06-cloud-devops-sre/README.md)
- [07 — AI/LLM Foundations](./07-ai-foundations/README.md)
- [08 — RAG & Retrieval Engineering](./08-rag/README.md)
- [09 — Agents, LangGraph & Multi-Agent Systems](./09-agents/README.md)
- [10 — MCP, A2A & Harness Engineering](./10-harness/README.md)
- [11 — AI Security, Safety & Governance](./11-security-governance/README.md)
- [12 — Evaluation, Observability & Reliability](./12-evaluation/README.md)
- [13 — Testing, QA & Assessment Engineering](./13-quality/README.md)
- [14 — Training, FDE & Technical Delivery](./14-delivery/README.md)

## Engineering philosophy

- Reliability before novelty.
- Explicit trade-offs before framework preference.
- Deterministic controls around probabilistic AI behavior.
- Authorization before data reaches the model.
- Component evaluation before end-to-end confidence.
- Reproducible examples before abstract advice.
- Production evidence before claims.
