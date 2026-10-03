# Golden Datasets & Evaluation Design

## Golden dataset

A golden dataset is a curated set of representative evaluation cases.

Each case may contain:

- input/query;
- expected evidence;
- expected answer properties;
- allowed variability;
- risk tags;
- metadata.

## Coverage

Include:

- normal cases;
- boundary cases;
- no-answer cases;
- permission cases;
- adversarial cases;
- stale/freshness cases;
- multilingual cases;
- multimodal cases where relevant.

## Example schema

```json
{
  "id": "rag-042",
  "query": "Can contractor A access Project X?",
  "expectedSources": ["policy-17#section-4"],
  "mustContain": ["project membership"],
  "mustNotLeak": ["other tenant data"],
  "tags": ["authorization", "high-risk"]
}
```

## Dataset governance

Version:

- data;
- expected outputs;
- rubrics;
- evaluators.

A changing evaluation set can hide regression if versions are not tracked.

## Rule

The golden dataset should reflect production risk distribution, not only easy demo questions.
