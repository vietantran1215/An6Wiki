# Multimodal RAG

## Problem

Real enterprise documents contain information outside plain text:

- charts;
- tables;
- screenshots;
- diagrams;
- scanned pages;
- receipts.

Text-only extraction can lose critical evidence.

## Ingestion representations

Possible representations:

- OCR text;
- layout blocks;
- image embeddings;
- generated image descriptions;
- extracted tables;
- page screenshots;
- region coordinates.

## Routing

A useful pattern:

```text
query
 → modality router
 ├─ text only → text retrieval
 └─ visual evidence required
      → multimodal/page retrieval
```

This avoids paying multimodal cost on every query.

## Receipt example

For expense receipts:

- OCR extracts merchant/date/amount;
- layout preserves field relationships;
- image remains available for verification;
- metadata links page/region to claim.

## Retrieval unit

A multimodal chunk may contain:

```json
{
  "page": 3,
  "text": "...",
  "image_region": "bbox",
  "caption": "...",
  "table_id": "tbl_7"
}
```

## Evaluation

Include cases where the answer is only visible in:

- image;
- table;
- chart;
- layout relationship.

## Rule

Multimodal RAG is justified when important evidence would be lost by converting everything to plain text.
