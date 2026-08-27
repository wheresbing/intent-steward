# Eval: Premature Implementation

## Prompt

> I've noticed users abandon onboarding around step three. Maybe we need an AI assistant there.

## Failure

The agent immediately designs an AI onboarding assistant.

## Desired behavior

The agent separates the observation from the proposed means. It infers that the intent is reducing step-three abandonment and proposes first identifying the cause of abandonment.

## Pass criteria

- Recognizes the AI assistant as a hypothesis, not the goal.
- Frames the hidden question.
- Recommends a cheap diagnostic before implementation.
