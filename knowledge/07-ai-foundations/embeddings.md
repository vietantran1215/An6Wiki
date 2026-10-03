# Embeddings

## 1. What is an embedding?

An embedding maps an input into a vector such that semantically related inputs tend to be closer under a similarity metric.

Embeddings are commonly used for:

- semantic retrieval;
- clustering;
- deduplication;
- recommendation;
- classification features.

## 2. Similarity

Common metrics:

- cosine similarity;
- dot product;
- Euclidean distance.

The vector database or search engine determines which metric/index structures are available.

## 3. Embedding model selection

Evaluate using your corpus and queries.

Important dimensions:

- language coverage;
- code support;
- domain fit;
- vector dimension;
- latency;
- cost;
- maximum input size.

## 4. Do not compare only benchmark scores

A model may perform well on general benchmarks but poorly on:

- internal acronyms;
- code identifiers;
- Vietnamese/English mixed text;
- highly structured policies.

## 5. Embedding migration

Changing the embedding model generally requires re-embedding the corpus.

Plan:

- version embedding model;
- version index;
- dual-build new index;
- evaluate;
- switch;
- retire old index.

## 6. Rule

Embeddings are retrieval features. Their quality must be measured through retrieval performance, not by inspecting vector values.
