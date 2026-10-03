# Canonical Code Patterns

## 1. Exponential backoff with full jitter

```ts
function sleep(ms: number) {
  return new Promise((resolve) => setTimeout(resolve, ms));
}

export async function retry<T>(
  fn: () => Promise<T>,
  maxAttempts = 4,
  baseMs = 200,
): Promise<T> {
  let lastError: unknown;

  for (let attempt = 0; attempt < maxAttempts; attempt++) {
    try {
      return await fn();
    } catch (error) {
      lastError = error;
      const ceiling = baseMs * 2 ** attempt;

      // Full jitter reduces synchronized retry storms.
      const delay = Math.random() * ceiling;
      await sleep(delay);
    }
  }

  throw lastError;
}
```

## 2. Bounded concurrency

```ts
import pLimit from "p-limit";

const limit = pLimit(5);

export async function processItems(items: string[]) {
  return Promise.all(
    items.map((item) =>
      limit(async () => processOne(item)),
    ),
  );
}

async function processOne(item: string) {
  return item.toUpperCase();
}
```

## 3. Async FastAPI boundary

```python
from fastapi import FastAPI
import httpx

app = FastAPI()

@app.get("/profile/{user_id}")
async def get_profile(user_id: str):
    # Async network I/O avoids blocking the event loop.
    async with httpx.AsyncClient(timeout=3.0) as client:
        response = await client.get(
            f"https://example.internal/users/{user_id}"
        )
        response.raise_for_status()
        return response.json()
```

## 4. Permission-aware retrieval

```python
def build_retrieval_filter(principal, requested_project_id: str):
    # Authorization comes from trusted identity context,
    # not directly from user-supplied metadata.
    if requested_project_id not in principal.allowed_project_ids:
        raise PermissionError("Project access denied")

    return {
        "tenant_id": principal.tenant_id,
        "project_id": requested_project_id,
    }
```

## 5. Bounded agent loop

```python
MAX_STEPS = 6

def run_agent(state):
    for _ in range(MAX_STEPS):
        action = plan_next_action(state)

        if action.type == "finish":
            return action.result

        state = execute_and_observe(state, action)

    return {
        "status": "fallback",
        "reason": "step_budget_exhausted",
    }
```

## 6. Risk-gated tool execution

```python
def execute_tool(tool_call, principal):
    policy = authorize(tool_call, principal)

    if not policy.allowed:
        raise PermissionError(policy.reason)

    if policy.requires_human_approval:
        return {
            "status": "approval_required",
            "tool_call": tool_call,
        }

    return invoke(tool_call)
```

## 7. Transactional outbox

```text
BEGIN
  update domain row
  insert outbox event
COMMIT

publisher:
  select unsent events
  publish
  mark sent
```

## 8. Expand → migrate → contract

1. Expand schema compatibly.
2. Deploy code that supports both versions.
3. Migrate data.
4. Verify.
5. Remove old behavior only when every consumer is safe.
