# Observability & SRE

## Observability signals

Use:

- logs;
- metrics;
- traces;
- domain/business signals.

## SLI and SLO

An SLI is a measured signal.

An SLO is the target.

Example:

```text
SLI: successful claim submissions / valid submission attempts
SLO: >= 99.9% over 30 days
```

## Error budget

If SLO is 99.9%, the remaining 0.1% is the error budget.

The budget connects reliability with release velocity.

## Tracing

Distributed tracing should propagate context across:

- API calls;
- queues;
- databases where supported;
- AI model calls;
- tool invocations.

## OpenTelemetry example

```python
from opentelemetry import trace

tracer = trace.get_tracer(__name__)

def rerank_documents(query, docs):
    with tracer.start_as_current_span("rag.rerank") as span:
        span.set_attribute("rag.candidate_count", len(docs))
        return reranker.rank(query, docs)
```

## Alert quality

Alert on user-impacting symptoms and fast error-budget burn, not every internal anomaly.

## Rule

Observability is part of the architecture. If a production failure cannot be explained from telemetry, the system is under-instrumented.
