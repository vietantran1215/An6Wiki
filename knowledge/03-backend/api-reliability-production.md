# API Reliability & Production Readiness

## 1. Production readiness is a system property

A correct endpoint is not enough.

A production API must handle:

- overload;
- slow dependencies;
- deployment transitions;
- malformed input;
- duplicate requests;
- partial failures;
- observability;
- rollback.

## 2. Request path budget

Example latency budget:

```text
Total API target: 500 ms
  auth/policy:       30 ms
  database:         120 ms
  dependency A:    150 ms
  application work: 50 ms
  network/headroom:150 ms
```

Budgets force explicit dependency timeouts.

## 3. Health endpoints

Readiness and liveness answer different questions.

- liveness: should the process be restarted?
- readiness: should it receive traffic?

## 4. Graceful shutdown

On shutdown:

1. stop accepting new work;
2. finish or safely abort in-flight work;
3. stop consumers;
4. flush telemetry;
5. close DB/broker connections.

## 5. Correlation

Attach a request/correlation ID across:

- API;
- database logs where possible;
- downstream calls;
- queue messages;
- traces.

## 6. Example middleware

```python
import uuid
from fastapi import Request

@app.middleware("http")
async def correlation_id(request: Request, call_next):
    correlation_id = request.headers.get(
        "X-Correlation-ID",
        str(uuid.uuid4()),
    )

    response = await call_next(request)
    response.headers["X-Correlation-ID"] = correlation_id
    return response
```

## 7. Release checklist

- schema migrations are backwards compatible;
- feature flags exist for risky changes;
- alerts cover user-facing failure;
- rollback path is tested;
- dependencies have timeouts;
- writes are retry-safe;
- critical actions are audited.
