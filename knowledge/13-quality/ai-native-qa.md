# AI-Native QA

## Scope

AI-native QA applies AI to quality work while also testing AI systems themselves.

## AI-assisted QA capabilities

- requirement analysis;
- ambiguity detection;
- test-case generation;
- test-data generation;
- defect clustering;
- log/trace analysis;
- flaky-test analysis;
- code/test review.

## Testing AI systems

Probabilistic systems require:

- golden datasets;
- rubrics;
- evaluator calibration;
- adversarial cases;
- drift monitoring;
- production feedback.

## QA copilot architecture

```text
Requirements / Jira / Confluence / Figma / API specs / code
                ↓
          permission-aware RAG
                ↓
        test-design assistant
                ↓
 deterministic validation / templates
                ↓
        test artifacts + evidence
```

## Human oversight

Generated tests still need validation for:

- requirement correctness;
- business risk;
- duplicated cases;
- false assumptions;
- missing negative tests.

## Agentic QA

An agent may:

- inspect requirements;
- retrieve domain rules;
- generate candidate tests;
- run automation;
- inspect failures;
- propose defects.

High-impact actions such as closing defects or approving releases should remain policy controlled.

## Rule

AI should increase QA leverage, not remove traceability or accountability.
