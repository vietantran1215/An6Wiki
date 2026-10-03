# Redis & Caching

## 1. Why cache?

Caching reduces latency and dependency load.

But cache introduces a second copy of data, so consistency becomes a design problem.

## 2. Cache-aside

```text
read request
 → check cache
 → miss?
    → load DB
    → populate cache
 → return
```

```python
async def get_user(user_id: str):
    cached = await redis.get(f"user:{user_id}")
    if cached:
        return json.loads(cached)

    user = await repo.get(user_id)

    if user:
        await redis.setex(
            f"user:{user_id}",
            300,
            json.dumps(user),
        )

    return user
```

## 3. Invalidation

Common strategies:

- TTL only;
- explicit delete on write;
- versioned cache keys;
- event-driven invalidation.

"The two hard things are naming and cache invalidation" is funny because stale data is a correctness problem, not only a performance issue.

## 4. Cache stampede

When a hot key expires, many callers may simultaneously hit the database.

Mitigations:

- jittered TTL;
- single-flight locking;
- stale-while-revalidate;
- prewarming.

## 5. Redis beyond caching

Redis may also support:

- rate limiting;
- short-lived sessions;
- distributed coordination;
- streams;
- queues;
- counters.

Do not let Redis become an ungoverned shared global state store.

## 6. Failure behavior

Ask:

- Can the system operate if Redis is down?
- Is stale data acceptable?
- Is the cache authoritative?
- What happens after eviction?
- How much memory can the cache consume?

## 7. Decision rule

Cache only data whose latency/load benefit outweighs consistency and operational complexity.
