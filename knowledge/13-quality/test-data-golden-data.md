# Test Data & Golden Data

## Test data categories

- synthetic normal cases;
- boundary cases;
- invalid cases;
- production-like anonymized cases;
- adversarial cases;
- golden evaluation cases.

## Golden data

Golden data has a stable expected interpretation.

For RAG:

- query;
- relevant document/chunk;
- answer requirements;
- forbidden leakage.

For multimodal documents:

- PDF page;
- table/image region;
- expected extracted fields;
- expected citation.

## Example

```json
{
  "caseId": "receipt-017",
  "source": "receipt_017.pdf",
  "expected": {
    "merchant": "Example Cafe",
    "amount": 18.50,
    "currency": "USD"
  },
  "evidence": {
    "page": 1,
    "region": "total"
  }
}
```

## Privacy

Do not casually copy production PII into test environments.

Use:

- synthetic generation;
- masking;
- tokenization;
- approved anonymization.

## Rule

Good test data represents production risk while remaining reproducible and governed.
