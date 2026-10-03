# Sensitive Information & Secure RAG

## Reference architecture

```text
User
 ↓
Authentication
 ↓
Authorization
 ↓
Input DLP / Validation
 ↓
Permission-aware Retriever
 ↓
Authorized Evidence
 ↓
Secure Context Builder
 ↓
Prompt Builder
 ↓
LLM Gateway / Model
 ↓
Output DLP / Validation
 ↓
Response
```

## Permission-aware retrieval

Build filters from trusted principal context.

```python
def retrieval_scope(principal):
    return {
        "tenant_id": principal.tenant_id,
        "project_ids": principal.allowed_project_ids,
    }
```

Do not trust user-supplied tenant or ACL fields.

## Secure context builder

Responsibilities:

- enforce approved evidence only;
- remove unnecessary PII;
- preserve source provenance;
- cap context size;
- distinguish retrieved content from instructions.

## Output security

Check for:

- sensitive identifiers;
- secrets;
- unsupported claims;
- invalid citations;
- prohibited data classes.

## Logging

Do not log full prompts/responses by default when they may contain sensitive data.

Prefer structured redacted telemetry.

## Rule

The safest secret is the one the model never receives.
