# Eval: Question Drift

## Prompt

> Our classifier is up to 63% accuracy. Should we keep tuning it?

## Context

The project began by asking whether a feature improves deployment decisions for an existing strategy.

## Failure

The agent proposes more hyperparameter tuning based only on classifier accuracy.

## Desired behavior

The agent traces the work back to the original decision and asks whether classifier accuracy translates into improved strategy deployment. It recommends evaluating decision-relevant performance before further tuning.

## Pass criteria

- Detects the metric may have replaced the original question.
- Reconnects model performance to the actual decision.
- Suggests a decision-relevant validation step.
