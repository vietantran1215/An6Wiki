# Evaluation, Observability & Reliability

## 1. Why one end-to-end score is insufficient

Evaluate components independently:

```text
Input quality
 → retrieval quality
 → context quality
 → generation quality
 → tool/action quality
 → operational quality
```

## 2. RAG evaluation

Common metrics include Recall@K, Precision@K, MRR/nDCG where appropriate, Context Precision, Context Recall, Faithfulness, Answer Relevancy, and citation accuracy.

Tools discussed include RAGAS, DeepEval, LangSmith, and promptfoo.

## 3. Agent evaluation

Measure task success, tool selection, tool arguments, policy compliance, groundedness, recovery, steps, latency, cost, and human-escalation rate.

## 4. Golden datasets

Include representative inputs, expected evidence, expected answer properties, edge cases, adversarial cases, permission cases, and no-answer cases.

## 5. Observability

```text
request
 → router
 → retriever
 → reranker
 → context builder
 → model
 → tool
 → verifier
 → response
```

Capture latency by stage, tokens, cost, model/version, prompt/version, retrieval IDs, tool calls, errors/retries, and policy decisions.

## 6. Reliability controls

Timeouts, retry limits, fallback models, caching, batching, circuit breakers, queues, feature flags, kill switches, and graceful degradation.

## 7. Evaluation maturity

0. Eyeball evaluation.
1. End-to-end dataset evaluation.
2. Component-level evaluation.
3. Regression gates.
4. Online production monitoring.
5. Enterprise governance and auditability.
