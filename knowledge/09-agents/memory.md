# Memory: Short-Term vs Long-Term

## Short-term memory

Short-term memory is the state needed inside a conversation or workflow.

Examples:

- current goal;
- prior tool results;
- unresolved questions;
- current plan;
- selected entity.

It often belongs in checkpointed runtime state.

## Long-term memory

Long-term memory persists knowledge across sessions.

Examples:

- stable preferences;
- project facts;
- learned user settings;
- historical decisions.

## Memory is not raw conversation replay

A robust memory system may:

1. extract candidate facts;
2. classify sensitivity;
3. validate;
4. version;
5. retrieve only relevant memory later.

## Memory retrieval

Treat memory like another retrieval system:

- query;
- relevance;
- freshness;
- scope;
- permission.

## Example memory record

```python
from pydantic import BaseModel
from datetime import datetime

class MemoryRecord(BaseModel):
    subject: str
    fact: str
    source_ref: str
    created_at: datetime
    expires_at: datetime | None = None
    confidence: float
```

## Risks

- stale preferences;
- conflicting facts;
- oversharing;
- privacy leakage;
- incorrect inferred memory;
- memory poisoning.

## Rule

Persist only information that provides future value and has a clear lifecycle. More memory is not automatically better.
