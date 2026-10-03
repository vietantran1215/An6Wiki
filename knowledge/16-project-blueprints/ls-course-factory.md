# LS Course Factory

## Problem

Training demand is usually transformed manually into disconnected artifacts:

- syllabus;
- learning objectives;
- project;
- requirements;
- architecture;
- backlog;
- assessments.

This creates inconsistency and weak traceability.

## Goal

Build a governed EdTech engineering platform that converts training demand into a traceable delivery package.

## Artifact flow

```text
Training Need
 → Competency Model
 → Syllabus
 → Capstone
 → URD / SRS
 → Architecture
 → User Stories
 → Acceptance Criteria
 → GitLab Backlog
 → Learning / Assessment Evidence
```

## Orchestration model

Use deterministic macro-orchestration for the known lifecycle.

Use bounded agents only inside open-ended steps.

Example:

```text
LangGraph workflow
  ├─ requirements agent
  ├─ architecture agent
  ├─ assessment agent
  └─ verifier
```

Top-level autonomous systems may communicate through A2A-style task contracts.

GitLab integration is exposed through a bounded MCP server.

## Technical baseline

Representative stack:

- FastAPI;
- Pydantic;
- SQLAlchemy;
- Alembic;
- PostgreSQL/pgvector;
- React/TypeScript;
- Docker Compose;
- SSE;
- RAGAS/DeepEval;
- hybrid retrieval;
- HITL.

## Key quality property

Every generated artifact must trace back to upstream intent.

A user story without a requirement, or a test without an acceptance criterion, is a traceability defect.

## Rule

Use AI to accelerate artifact creation, but deterministic workflow and verification should preserve governance.
