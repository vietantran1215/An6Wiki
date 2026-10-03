# Tool Security & Excessive Agency

## Excessive agency

Risk increases when the model has:

- broad tool access;
- powerful credentials;
- irreversible actions;
- weak approval;
- long autonomous loops.

## Least privilege

Tools should receive the minimum capability required.

Prefer:

```text
approve_claim(claim_id)
```

over:

```text
database_execute(sql)
```

## Side-effect classes

Classify tools:

- read-only;
- reversible write;
- irreversible write;
- financial;
- external communication;
- infrastructure/admin.

Higher classes require stronger approval and auditing.

## Example risk gate

```python
def execution_mode(tool):
    if tool.risk in {"financial", "irreversible", "admin"}:
        return "human-approval"
    return "automatic"
```

## Other controls

- idempotency;
- resource version check;
- dry-run;
- rate limits;
- transaction boundaries;
- scoped credentials;
- audit.

## Rule

Agent autonomy should be proportional to reversibility, confidence, and business impact.
