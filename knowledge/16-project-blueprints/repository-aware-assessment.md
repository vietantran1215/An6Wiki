# Repository-Aware Engineering Assessment

## Goal

Assess engineering competency using real code evidence rather than isolated multiple-choice questions.

## Inputs

- Git repository;
- architecture/specification;
- competency framework;
- learner PRs;
- test results.

## Ingestion

For source code:

- language detection;
- AST/code-aware chunking;
- symbol metadata;
- file/module ownership;
- dependency graph.

## Retrieval

```text
question / competency
 → lexical symbol search
 → code embedding search
 → graph traversal
 → reranking
 → evidence bundle
```

## Assessment workflow

```text
Competency
 → generate evidence-seeking question
 → learner answer
 → retrieve repo evidence
 → deterministic checks
 → rubric evaluation
 → trainer review where needed
```

## Deterministic grading

Do not let the LLM invent repository facts.

Examples of deterministic evidence:

- function exists;
- test passes;
- dependency imported;
- branch coverage;
- API route registered;
- migration present.

## LLM role

Use the model for:

- explanation quality;
- architecture reasoning;
- trade-off analysis;
- follow-up questions.

## Rule

Use code and test evidence for objective claims; use LLM evaluation for reasoning dimensions that genuinely require judgment.
