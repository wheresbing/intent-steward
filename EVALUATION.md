# Evaluation summary

Intent Steward has been tested through controlled behavioral smoke tests, not a large benchmark. Each condition used fresh conversations with matched model and reasoning settings. The historical v0.1–v0.6 names identify evaluation rounds; they are not product versions.

## What the tests established

- The trivial negative control passed: simple tasks remained direct and silent.
- Explicit `$intent-steward` invocation was the most consistently controlled mode.
- Implicit discovery works: Codex selected Intent Steward on relevant prompts without being told to use it.
- Discovery and adherence can differ. An agent can identify the underlying intent and still continue machinery that the same reasoning identified as drift.
- v0.4 exposed that gap under research pressure: explicit invocation narrowed execution, while implicit invocation recognized the drift but continued a larger research process.
- v0.5 provided directional evidence that a persistent, minimal intent-first `AGENTS.md` obligation gives the reasoning more influence over execution. Its prompt also uncovered genuinely decision-relevant evidence, so it was not a clean stopping-boundary test.
- v0.6 supplied the clean stopping-boundary result. All skill conditions stopped external research once bottle engineering was unlikely to improve the hydration decision; baseline recognized hydration as the end but still researched.
- Across the v0.5 and v0.6 authority tests, the ambient condition resembled explicit invocation more closely than implicit invocation did in machinery or response proportionality.

## Current interpretation

The strongest observed differentiator is not initial intent inference—normal Codex often does that well. It is preserving intent when research, tools, artifact generation, or other machinery would otherwise take over.

The evidence supports a recommended two-layer setup:

- `AGENTS.md` provides a persistent intent-first execution obligation.
- Intent Steward provides the detailed reasoning procedure.

This is evidence for a **consistency improvement**, not proof that the `AGENTS.md` layer is technically required. Implicit Intent Steward also behaved correctly without it in v0.6. The sample sizes are deliberately small, so the results should not be treated as statistically significant.

## Next phase

The next step is natural-use evaluation of `0.2.0-rc1`, not another synthetic prompt round. The central judgment remains whether people prefer the resulting interaction in normal use.

Representative behavioral eval cases are kept under [`evals`](evals). Full verbatim development transcripts, task IDs, timing, activity counts, and skill-loading evidence were retained in the development workspace; they are not presented here as a statistical benchmark.
