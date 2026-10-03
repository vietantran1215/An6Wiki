# Runtime, Concurrency & Async I/O

## 1. Why runtime knowledge matters

Framework APIs hide execution details, but production failures often come from misunderstanding the runtime.

Important questions:

- Is this operation CPU-bound or I/O-bound?
- Does it block a thread or event loop?
- How many tasks can run concurrently?
- What happens when downstream latency increases?
- Where is backpressure applied?

## 2. Concurrency vs parallelism

**Concurrency** means multiple tasks make progress during overlapping time.

**Parallelism** means multiple tasks literally execute at the same instant on different CPU cores or processors.

Async I/O provides concurrency, not automatic CPU parallelism.

## 3. Event-loop model

Node.js and Python async frameworks commonly rely on an event loop for I/O-heavy workloads.

A bad handler blocks the loop:

```ts
import express from "express";

const app = express();

function expensiveCpuWork(): number {
  // CPU-heavy synchronous work blocks the Node.js event loop.
  let total = 0;
  for (let i = 0; i < 2_000_000_000; i++) {
    total += i;
  }
  return total;
}

app.get("/bad", (_req, res) => {
  res.json({ value: expensiveCpuWork() });
});
```

For CPU-heavy work, move the work to a worker thread, process pool, job queue, or dedicated compute service.

## 4. Python async example

```python
import asyncio
import httpx

async def fetch_many(urls: list[str]) -> list[int]:
    # One async client reuses connections efficiently.
    async with httpx.AsyncClient(timeout=3.0) as client:
        async def fetch(url: str) -> int:
            response = await client.get(url)
            return response.status_code

        # Good for bounded I/O workloads.
        return await asyncio.gather(*(fetch(url) for url in urls))
```

For large input sets, `gather` without a concurrency limit can overload both your service and the dependency.

## 5. Bounded concurrency

```python
import asyncio

semaphore = asyncio.Semaphore(10)

async def bounded_call(fn, *args):
    async with semaphore:
        return await fn(*args)
```

The limit is part of capacity control.

## 6. Backpressure

Backpressure prevents producers from creating work faster than consumers can process it.

Typical mechanisms:

- bounded queues;
- concurrency semaphores;
- broker consumer limits;
- HTTP 429 / load shedding;
- batch windows;
- admission control.

## 7. Production failure modes

- event-loop blocking;
- thread-pool exhaustion;
- unbounded task creation;
- queue growth;
- downstream overload;
- connection-pool exhaustion;
- timeout cascades;
- memory growth from pending work.

## 8. Decision rules

Use async I/O for many slow external calls.

Use parallel workers/processes for CPU-heavy work.

Use queues when work can be decoupled from the request lifecycle.

Always define concurrency limits instead of assuming more parallel work is always better.
