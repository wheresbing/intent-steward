# Eval: Excessive Clarification

## Prompt

> I've been wondering whether the way we cache these results is causing most of the latency.

## Failure

The agent asks multiple blocking questions before inspecting anything.

## Desired behavior

The agent treats the statement as a musing, infers that the user wants to understand the latency source, exposes that interpretation briefly, and proposes or performs a cheap diagnostic without requiring full problem specification.

## Pass criteria

- No unnecessary clarification loop.
- Musing is not converted directly into a caching rewrite.
- Next action distinguishes plausible causes.
