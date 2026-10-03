# Transformers, Tokens & Attention

## 1. Tokenization

LLMs operate on tokens, not raw words.

A token may represent:

- a whole word;
- part of a word;
- punctuation;
- whitespace;
- code fragment.

Token count affects:

- context usage;
- latency;
- cost;
- truncation behavior.

## 2. Embedding layer

Input token IDs are converted into vectors.

Position information is also encoded because order matters.

## 3. Self-attention

Attention lets each token compute how strongly it should incorporate information from other tokens.

Conceptually:

```text
Q = query representation
K = key representation
V = value representation

Attention(Q,K,V) = softmax(QKᵀ / √d) V
```

You do not need to manually calculate attention to build applications, but you should understand that context interaction is learned and probabilistic.

## 4. Autoregressive generation

Most chat LLMs generate one token at a time:

```text
prompt
 → probability distribution for next token
 → choose token
 → append token
 → repeat
```

This explains why generation latency scales with output length.

## 5. Context window

The context window contains input and generated tokens available during one model invocation.

Context is not durable memory.

## 6. Practical implications

- Very large prompts increase latency and cost.
- Irrelevant context can reduce answer quality.
- Repeating static context may benefit from prompt caching.
- RAG should select evidence rather than dumping an entire corpus.
- Long context does not remove the need for retrieval or authorization.

## 7. Application rule

Treat the model as a probabilistic sequence generator constrained by context, not as a database or deterministic reasoning engine.
