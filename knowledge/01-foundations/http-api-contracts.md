# HTTP, APIs & Contracts

## 1. HTTP is a protocol contract

An API is not only a URL and JSON payload. A reliable contract includes:

- method semantics;
- status codes;
- headers;
- authentication;
- authorization;
- caching;
- idempotency;
- pagination;
- error shape;
- versioning;
- timeout expectations.

## 2. Method semantics

Common intent:

- `GET` — read;
- `POST` — create/execute;
- `PUT` — full replacement;
- `PATCH` — partial update;
- `DELETE` — delete.

Method choice affects retry safety and caching behavior.

## 3. Idempotency

A client may retry because the network response was lost even though the server successfully processed the first request.

Use an idempotency key for important retryable writes.

```python
from fastapi import FastAPI, Header, HTTPException

app = FastAPI()
processed: dict[str, dict] = {}

@app.post("/payments")
async def create_payment(
    amount: int,
    idempotency_key: str = Header(alias="Idempotency-Key"),
):
    if idempotency_key in processed:
        return processed[idempotency_key]

    # Production code should persist this transactionally.
    result = {"payment_id": "pay_123", "amount": amount}
    processed[idempotency_key] = result
    return result
```

## 4. Error contracts

Prefer stable structured errors.

```json
{
  "code": "CLAIM_NOT_APPROVABLE",
  "message": "Claim must be in submitted state.",
  "details": {
    "claimId": "clm_123",
    "currentState": "draft"
  }
}
```

The client should not parse human prose to determine program behavior.

## 5. Pagination

Offset pagination is simple but can be unstable under concurrent writes.

Cursor/keyset pagination provides better consistency for large or frequently changing datasets.

## 6. API evolution

Prefer backwards-compatible evolution:

- add optional fields;
- avoid silently changing field meaning;
- tolerate unknown fields where appropriate;
- version breaking changes explicitly.

## 7. Production concerns

- request size limits;
- timeouts;
- request IDs;
- correlation IDs;
- rate limits;
- schema validation;
- audit logging;
- PII-safe logs;
- dependency failure mapping.

## 8. Decision rule

A good API is a product contract. It should allow independent teams and systems to evolve without requiring shared implementation knowledge.
