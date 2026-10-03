# FastAPI Production Stack

## Baseline stack

A recurring production stack:

- FastAPI;
- Pydantic;
- SQLAlchemy;
- Alembic;
- PostgreSQL;
- pytest;
- httpx;
- OpenTelemetry;
- Docker;
- CI/CD.

## Project structure

```text
app/
  api/
  application/
  domain/
  infrastructure/
  observability/
tests/
migrations/
```

## Configuration

Validate configuration at startup.

```python
from pydantic_settings import BaseSettings

class Settings(BaseSettings):
    database_url: str
    environment: str = "local"

settings = Settings()
```

## Production checklist

- startup validation;
- structured logging;
- request correlation;
- async-safe dependencies;
- DB pool sizing;
- migrations;
- health/readiness;
- auth;
- rate limits;
- tests;
- graceful shutdown.

## Rule

The goal is not "use FastAPI." The goal is a reproducible, observable, secure Python service with explicit boundaries.
