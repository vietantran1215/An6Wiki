# RAG Evaluation Maturity

## Level 0 — Eyeball

People manually try a few questions.

Useful for initial exploration, but it is not a regression system.

## Level 1 — End-to-end dataset

Create a golden dataset and score final answers.

Measure:

- answer correctness/relevance;
- faithfulness;
- citation quality.

Problem: failures are still hard to localize.

## Level 2 — Component evaluation

Evaluate individual stages:

- retrieval;
- reranking;
- context construction;
- generation.

Example retrieval metrics:

- Recall@K;
- Precision@K;
- MRR;
- nDCG where appropriate.

## Level 3 — Regression gates

Run evaluation automatically on every meaningful change:

- prompt;
- model;
- chunking;
- embedding;
- retriever;
- reranker;
- corpus;
- policy.

Block release when critical metrics regress beyond accepted thresholds.

## Level 4 — Online production monitoring

Measure live behavior:

- latency;
- token usage;
- cost;
- retrieval misses;
- user feedback;
- fallback rate;
- no-answer rate;
- citation failures.

## Level 5 — Enterprise evaluation system

Add:

- versioned datasets;
- ownership;
- approval workflow;
- risk classification;
- auditability;
- trace linkage;
- drift review;
- production incident feedback.

## Golden dataset design

Include:

- normal questions;
- difficult questions;
- no-answer cases;
- adversarial cases;
- permission cases;
- stale/freshness cases;
- multimodal cases where relevant.

## Rule

An end-to-end score answers "Did it work?"

Component evaluation answers "Why did it fail?"
