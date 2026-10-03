# Python & FastAPI Engineering

## 1. Why FastAPI

FastAPI is well suited to typed HTTP APIs, AI services, async I/O, and rapid production development.

Its strengths come from:

- ASGI;
- Python type hints;
- Pydantic;
- OpenAPI generation;
- async support.

## 2. Layering

```text
router
 → application service
 → domain logic
 → repository / external client
```

Avoid putting database queries and business logic directly inside route functions.

## 3. Example

```python
from fastapi import APIRouter, Depends
from pydantic import BaseModel

router = APIRouter()

class CreateClaim(BaseModel):
    amount: int
    description: str

@router.post("/claims")
async def create_claim(
    request: CreateClaim,
    service = Depends(get_claim_service),
):
    # Route handles transport; service owns use-case logic.
    return await service.create(request)
```

## 4. Sync vs async

Use `async def` when the request path performs asynchronous I/O with compatible drivers.

Do not call slow synchronous libraries inside the event loop without moving them to a thread/process.

## 5. Production baseline

- Pydantic validation;
- SQLAlchemy;
- Alembic;
- structured errors;
- async-aware DB/session handling;
- health/readiness endpoints;
- tracing;
- graceful shutdown;
- configuration validation;
- tests;
- Docker;
- CI/CD.

## 6. Common mistakes

- global mutable state;
- unbounded background tasks;
- blocking libraries in async routes;
- DB session leakage;
- no transaction boundaries;
- business logic in routers;
- weak error contracts.

## 7. Decision rule

FastAPI is an API framework, not an architecture. Production quality still depends on boundaries, data ownership, security, tests, telemetry, and deployment discipline.
