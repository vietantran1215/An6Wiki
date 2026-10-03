# Model Types, Training & Fine-Tuning

## Foundation model

A foundation model is pretrained on broad data and can support many downstream tasks.

## Pretraining

Pretraining teaches general statistical patterns by predicting tokens or related objectives at very large scale.

## Instruction tuning

Instruction tuning improves the ability to follow natural-language instructions.

## Preference/alignment tuning

Additional optimization can shape behavior toward human preferences, safety, or task quality.

## Fine-tuning

Fine-tuning adapts model behavior using additional examples.

Use cases:

- stable style;
- specialized output format;
- domain task behavior;
- smaller model specialization.

Fine-tuning is not the first solution for missing factual knowledge that changes frequently.

For changing knowledge, RAG is usually easier to update and inspect.

## RAG vs fine-tuning

Choose RAG when:

- knowledge changes;
- citations matter;
- access control matters;
- evidence must be inspectable.

Consider fine-tuning when:

- behavior/style is stable;
- many examples exist;
- latency/cost can improve using a smaller specialized model.

They can also be combined.

## Distillation and small language models

A smaller model may be preferable when:

- task scope is narrow;
- cost/latency matters;
- deployment is constrained;
- privacy favors local execution.

## Decision rule

Choose a model based on task quality, latency, cost, context length, privacy, modality, operational support, and evaluation—not benchmark reputation alone.
