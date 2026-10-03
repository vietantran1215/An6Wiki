# MCP Server: Development to Production

## 1. Define the capability boundary

An MCP server should expose bounded, intentional capabilities.

Good tool design:

- one clear responsibility;
- explicit input schema;
- explicit output shape;
- no hidden broad permissions;
- stable semantics.

## 2. Separate business logic from transport

A service may expose both MCP and REST.

Prefer:

```text
Domain / application service
        ↑
   business logic
      /      \
 REST API    MCP adapter
```

This avoids duplicating policy and behavior in each transport layer.

## 3. Local development

Verify:

- tool discovery;
- schema validation;
- success path;
- invalid input;
- dependency timeout;
- permission denial;
- idempotent retry behavior.

## 4. Authentication and authorization

Authentication determines the caller.

Authorization should evaluate:

- principal;
- tenant;
- resource;
- action;
- policy.

Do not rely on the model to decide whether a tool call is allowed.

## 5. Production controls

Each tool should have:

- strict schema validation;
- least-privilege credentials;
- timeout;
- retry policy;
- rate limit;
- audit event;
- structured error contract;
- observability;
- approval policy for high-risk actions.

## 6. Deployment

A production deployment needs:

- reproducible build;
- environment configuration;
- secret management;
- health/readiness checks;
- logging and tracing;
- versioning;
- rollback path.

If REST is also exposed, normal API production concerns still apply.

## 7. Agent integration

The agent runtime should own:

- which tools are visible;
- which tools are allowed for the current principal;
- tool-call budgets;
- retry behavior;
- human approval;
- audit correlation.

## 8. Failure model

Expect:

- malformed tool arguments;
- unavailable dependencies;
- duplicate calls;
- slow calls;
- partially completed side effects;
- stale authorization context;
- model-generated unsafe requests.

Design the MCP layer like a privileged production API, not a convenience plugin.
