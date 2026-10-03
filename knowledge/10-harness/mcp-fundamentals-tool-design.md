# MCP Fundamentals & Tool Design

## MCP model

MCP exposes capabilities such as:

- tools;
- resources;
- prompts.

A host/client connects to an MCP server to discover and invoke those capabilities.

## MCP is not business authorization

The server still needs:

- identity;
- access policy;
- schema validation;
- rate limiting;
- audit;
- timeouts.

## Tool design

A good tool has:

- narrow responsibility;
- explicit schema;
- stable semantics;
- bounded side effects;
- machine-readable errors.

## Example conceptual tool

```python
class ApproveClaimInput(BaseModel):
    claim_id: str
    expected_version: int

async def approve_claim(args: ApproveClaimInput, principal):
    authorize(principal, "claim.approve", args.claim_id)

    # expected_version provides optimistic concurrency protection.
    return await claim_service.approve(
        claim_id=args.claim_id,
        expected_version=args.expected_version,
        actor_id=principal.id,
    )
```

## Do not expose generic primitives

Dangerous:

```text
execute_sql(query)
shell(command)
http_request(url, method, body)
```

Prefer domain-bounded operations.

## Rule

An MCP tool should look like a production API capability, not a remote-code-execution shortcut.
