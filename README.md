# Intent Steward

**Help AI agents preserve the connection between tasks and the human purpose they serve.**

> Do not make users perfectly specify their intent before helping them. Help them discover it while doing the work.
>
> **Infer → Expose → Refine → Act → Re-evaluate**

Intent Steward is a lightweight protocol and agent skill for working with latent, evolving, or partially articulated user intent.

LLMs are often very good at the machinery of work: searching, coding, testing, summarizing, refactoring, documenting, and executing plans. But machinery is usually a means rather than the end.

A user may ask for a dashboard when the actual need is faster detection of strategy degradation. They may ask for a new indicator when the real question is whether a signal contains enough incremental information to justify building one. They may ask for more experiments after the original hypothesis has already stopped making sense.

Intent Steward teaches agents to treat intent as a **working hypothesis**, not a prerequisite the user must fully specify.

## Core behavior

1. **Infer** the likely underlying intent from the user's request, context, observations, and current work.
2. **Expose** that inference briefly and transparently when it materially affects the work.
3. **Refine** it using user corrections and new evidence without forcing clarification loops.
4. **Act** on the highest-information next step that serves the intent.
5. **Re-evaluate** when evidence, project direction, or assumptions change.

The agent should not repeatedly ask "what is your intent?" before proceeding. When reasonable, it should infer a working interpretation and continue.

## Three kinds of intent

- **Stated intent** — what the user explicitly asks for.
- **Inferred intent** — what the agent believes the request is in service of.
- **Proposed intent** — a potentially more useful framing the agent suggests.

The agent must never silently replace stated intent with proposed intent.

## Failure modes

### Means–ends inversion

The machinery becomes the apparent goal.

Example: improving a data pipeline long after the only meaningful question was whether the signal had enough information value to justify the pipeline.

### Question drift

The investigation slowly answers a different question from the one that motivated it.

Example:

`Does GEX improve strategy deployment?`
→ `Can GEX predict intraday returns?`
→ `Can this classifier reach 60% accuracy?`

The final metric may look impressive while no longer informing the original decision.

### Clarification tax

The agent forces the user to fully articulate intent through repeated questions before doing useful work.

Intent Steward prefers:

> "My working interpretation is X. That suggests Y is the most informative next step."

rather than:

> "Before I proceed, answer these five questions."

## Repository structure

```text
intent-steward/
├── README.md
├── AGENTS.md
├── spec/
│   └── INTENT_PROTOCOL.md
├── skills/
│   └── intent-steward/
│       └── SKILL.md
├── templates/
│   ├── INTENT.md
│   └── agents-snippet.md
├── examples/
│   ├── research.md
│   ├── debugging.md
│   ├── trading-research.md
│   └── software-feature.md
└── evals/
    ├── excessive-clarification.md
    ├── means-ends-inversion.md
    ├── premature-implementation.md
    └── question-drift.md
```

## Codex usage

Copy `skills/intent-steward/` into your project's `.agents/skills/intent-steward/` directory and optionally add the contents of `templates/agents-snippet.md` to your `AGENTS.md`.

For projects where intent should persist over time, copy `templates/INTENT.md` to the repository root.

The skill supports three conceptual modes:

- **FRAME** — infer and expose the working intent when beginning an exploratory line of work.
- **ADVANCE** — choose the highest-information next action relative to the current intent.
- **REVIEW** — reconcile evidence with beliefs and detect drift or means–ends inversion.

These modes do not require rigid command syntax. The agent should invoke the behavior when the situation warrants it.

## Design principles

- Intent is a hypothesis, not a contract.
- Infer before interrogating.
- Expose uncertainty without blocking useful work.
- Prefer decisions and uncertainty reduction over artifact production.
- Distinguish evidence, beliefs, assumptions, and goals.
- Ask "Why are we doing this next?"
- Optimize for information value before machinery quality.
- Revisit intent when evidence changes.
- Avoid philosophical overhead for trivial implementation tasks.

## Status

Early draft / v0.1 concept. The protocol, examples, and evals are intentionally small so behavior can be tested before adding more machinery.

## License

MIT
