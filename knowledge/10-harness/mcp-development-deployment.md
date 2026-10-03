# MCP Server: Development to Deployment

## Development stages

```text
domain capability
 → tool contract
 → local MCP server
 → validation
 → authn/authz
 → observability
 → remote transport
 → deployment
 → operations
```

## Separate domain from transport

```text
        Application Service
        /                 \
   REST Adapter        MCP Adapter
```

The MCP layer should not duplicate business logic already owned by the application service.

## Local transport

Local tools may use process-based transport.

Remote deployment needs a network transport plus standard API security and operations.

## Production controls

- authentication;
- authorization;
- origin/host validation;
- TLS;
- rate limit;
- timeout;
- bounded request size;
- structured errors;
- trace correlation;
- health checks;
- versioning.

## Deployment architecture

```text
Agent Host
   ↓ HTTPS
Gateway / Load Balancer
   ↓
MCP Server replicas
   ↓
Application services
   ↓
DB / queues / external systems
```

## Stateless scaling

Keep request handling stateless where possible.

Shared durable state belongs in an external store.

## Failure tests

Test:

- malformed input;
- unauthorized caller;
- dependency timeout;
- duplicate request;
- server restart;
- partial side effect;
- load spike.

## Rule

Deploy an MCP server with the same rigor as any privileged production API.
