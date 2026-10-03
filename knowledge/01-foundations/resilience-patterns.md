# Resilience Patterns

## 1. Reliability starts by assuming failure

Distributed systems fail partially.

A dependency may be:

- slow;
- unavailable;
- overloaded;
- returning stale data;
- returning invalid data;
- accepting a request but losing the response.

## 2. Timeout

Never allow unbounded waiting.

Timeouts should reflect:

- dependency SLO;
- caller latency budget;
- retry policy;
- business criticality.

## 3. Retry

Retry only when:

- the failure is plausibly transient;
- the operation is retry-safe or idempotent;
- retry will not worsen overload.

```ts
async function retry<T>(
  fn: () => Promise<T>,
  attempts = 4,
  baseMs = 200,
): Promise<T> {
  let lastError: unknown;

  for (let i = 0; i < attempts; i++) {
    try {
      return await fn();
    } catch (error) {
      lastError = error;

      // Exponential ceiling with full jitter.
      const ceiling = baseMs * 2 ** i;
      await new Promise((r) =>
        setTimeout(r, Math.random() * ceiling),
      );
    }
  }

  throw lastError;
}
```

## 4. Circuit breaker

A circuit breaker stops repeatedly calling a dependency that is already failing.

States:

```text
Closed → failures exceed threshold → Open
Open → cool-down → Half-open
Half-open → success → Closed
Half-open → failure → Open
```

## 5. Bulkhead

Separate resource pools so one failing dependency does not consume all capacity.

Examples:

- separate worker pools;
- separate queues;
- per-tenant concurrency limits;
- per-dependency connection pools.

## 6. Load shedding

Reject low-priority work when capacity is exhausted instead of allowing the entire service to collapse.

## 7. Graceful degradation

Fallback options:

- stale cache;
- reduced feature set;
- read-only behavior;
- alternative model/provider;
- queued asynchronous processing.

## 8. Failure-mode checklist

For every dependency ask:

- What is the timeout?
- Is retry safe?
- How many retries?
- What is the backoff?
- What is the fallback?
- Is there a circuit breaker?
- How is overload contained?
- What telemetry indicates degradation?

## 9. Anti-pattern

Combining long timeouts with multiple retries across several service layers can multiply latency and create retry storms.
