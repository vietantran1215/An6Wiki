# A2A & Agent Interoperability

## Purpose

Agent-to-Agent interoperability addresses collaboration between autonomous systems rather than model-to-tool access.

Conceptually:

- MCP: agent/model ↔ tools/resources;
- A2A: agent ↔ agent/task system.

## Task contract

An interoperable task exchange should define:

- task ID;
- intent;
- input artifact;
- expected output;
- status;
- cancellation;
- error;
- provenance.

## Example

```json
{
  "taskId": "task_123",
  "type": "security-review",
  "artifactRef": "repo://project/pr/42",
  "requiredChecks": [
    "authorization",
    "secret-leak",
    "dependency-risk"
  ]
}
```

## Trust

A remote agent must not automatically inherit the caller's privileges.

Define:

- caller identity;
- delegated scope;
- resource boundary;
- expiration;
- audit.

## Failure modes

- duplicate task;
- lost completion;
- stale status;
- incompatible capability;
- privilege escalation;
- unclear ownership.

## Rule

Interoperability requires task semantics and trust boundaries, not merely message passing.
