# Secure Enterprise RAG

## Security objective

The model should receive only information the current principal is authorized to access.

## Reference flow

```text
User
 ↓
Authentication
 ↓
Authorization context
 ↓
Input validation / DLP
 ↓
Permission-aware retrieval
 ↓
Authorized evidence
 ↓
Secure Context Builder
 ↓
Prompt Builder
 ↓
LLM Gateway / Model
 ↓
Output validation / DLP
 ↓
Response
```

## Authentication

Establish a trusted principal:

- user;
- service;
- workload identity.

## Authorization

Apply authorization before retrieval results reach the LLM.

Authorization can depend on:

- tenant;
- role;
- resource ownership;
- document ACL;
- project membership;
- data classification.

## Permission-aware retrieval

The application should derive filters from trusted identity context.

```python
def build_filter(principal, project_id: str):
    # Never trust a user-provided tenant or project filter as authority.
    if project_id not in principal.allowed_project_ids:
        raise PermissionError("Project access denied")

    return {
        "tenant_id": principal.tenant_id,
        "project_id": project_id,
    }
```

## Secure Context Builder

Responsibilities:

- keep only authorized evidence;
- remove unnecessary sensitive fields;
- preserve provenance;
- limit total context;
- separate trusted instructions from untrusted retrieved text;
- attach source metadata.

## LLM Gateway

Useful controls:

- approved model list;
- provider routing;
- retention/privacy policy;
- rate limits;
- cost limits;
- request logging policy.

## Output security

Validate:

- sensitive data leakage;
- schema;
- unsafe links/content;
- tool/action payload;
- citation provenance.

## Key rule

"Do not reveal confidential information" inside the prompt is a behavioral control, not an authorization mechanism.
