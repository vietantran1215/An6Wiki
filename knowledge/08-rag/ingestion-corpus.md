# Ingestion & Corpus Engineering

## 1. RAG starts before embeddings

Poor source ingestion cannot be fixed by a stronger LLM.

Corpus engineering includes:

- source discovery;
- parsing;
- cleaning;
- normalization;
- metadata;
- deduplication;
- versioning;
- access control;
- change detection.

## 2. Document types

Common sources:

- PDF;
- HTML;
- Markdown;
- Office documents;
- source code;
- database rows;
- tickets/wiki;
- images and scanned documents.

Each source type needs a parser that preserves useful structure.

## 3. Metadata

Useful metadata may include:

- source ID;
- tenant;
- project;
- document type;
- version;
- created/updated time;
- ACL;
- section;
- page;
- language;
- checksum.

## 4. Idempotent ingestion

```python
def ingestion_key(source_id: str, checksum: str) -> str:
    # The same unchanged source produces the same key.
    return f"{source_id}:{checksum}"
```

On re-ingestion:

- detect unchanged sources;
- update changed sources;
- remove obsolete chunks;
- preserve version traceability.

## 5. Corpus quality checks

Measure:

- parse failure rate;
- empty-document rate;
- duplicate rate;
- OCR quality where applicable;
- missing metadata;
- ACL coverage;
- stale-source age.

## 6. Security

Do not index content without preserving access-control information required for retrieval-time authorization.

## 7. Rule

A production RAG corpus is a governed data product, not a folder of files passed through a loader.
