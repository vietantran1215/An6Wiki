# Authentication & Authorization

## 1. Authentication

Authentication establishes identity.

Examples:

- password + session;
- JWT;
- OAuth 2.x;
- OIDC;
- service identity;
- workload identity.

## 2. Authorization

Authorization decides whether the principal can perform an action on a resource.

Useful models:

- RBAC — role-based;
- ABAC — attribute-based;
- relationship-based authorization;
- policy-based authorization.

## 3. JWT is not an authorization system

A token can carry claims, but the application still needs policy decisions.

```python
def can_approve_claim(user, claim) -> bool:
    return (
        "manager" in user.roles
        and user.tenant_id == claim.tenant_id
        and claim.status == "submitted"
        and claim.owner_id != user.id
    )
```

## 4. Refresh-token security

A robust design considers:

- rotation;
- revocation;
- reuse detection;
- device/session tracking;
- expiration;
- secure cookie/storage policy.

## 5. Enterprise identity

For enterprise systems, OIDC/OAuth often integrate with an external identity provider.

Important concepts:

- issuer;
- audience;
- scope;
- claims;
- JWKS;
- token lifetime;
- tenant;
- client credentials.

## 6. Authorization near data

Permission-aware RAG and enterprise APIs should enforce authorization before returning sensitive data.

Never retrieve everything and ask the model or frontend to filter later.

## 7. Auditability

High-risk actions should record:

- actor;
- action;
- resource;
- decision;
- policy/rule;
- timestamp;
- correlation ID;
- before/after state when appropriate.
