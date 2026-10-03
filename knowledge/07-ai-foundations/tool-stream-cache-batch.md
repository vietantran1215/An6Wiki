# Tool Calling, Streaming, Prompt Caching & Batch

## Tool calling

Tool calling allows a model to propose a typed operation.

```python
from pydantic import BaseModel

class SearchClaims(BaseModel):
    employee_id: str
    status: str | None = None
    limit: int = 20
```

The tool schema should be narrow and validated.

The model proposes arguments; the application authorizes and executes.

## Streaming

Streaming improves perceived latency by sending partial output before generation finishes.

Streaming complicates:

- moderation/output validation;
- structured parsing;
- cancellation;
- UI state;
- trace accounting.

## Prompt caching

Prompt caching is useful when a large prefix is reused.

Good candidates:

- long system instructions;
- stable policy text;
- tool definitions;
- shared reference context.

Caching dynamic user-specific secrets is a different risk profile and must respect provider semantics.

## Batch processing

Batch is useful for offline work:

- embeddings;
- evaluation;
- classification;
- extraction;
- large corpus enrichment.

A batch job should be restartable and idempotent.

## Example batch worker

```python
async def process_batch(items, embedder, repo):
    for item in items:
        if await repo.is_done(item.id):
            continue

        vector = await embedder.embed(item.text)
        await repo.save_vector(item.id, vector)
        await repo.mark_done(item.id)
```

## Decision rules

Use streaming for interactive UX.

Use caching for repeated stable prefixes.

Use batch when latency is not interactive and throughput/cost matter.

Use tool calling only with deterministic authorization and bounded capabilities.
