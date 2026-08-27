# Intent Steward

**Release candidate:** `0.2.0-rc1`

Intent Steward helps an AI keep track of **why a task exists**, not only what was requested.

It is useful when research, tools, implementation, or artifact creation could become disconnected from the decision or outcome they were meant to serve. It is not anti-research, anti-tools, or anti-detail:

> **Use machinery when it serves the end. Reduce it when it has become detached from the end.**

The core pattern is:

**Infer → Expose → Refine → Act → Re-evaluate**

## A simple example

Suppose you want to cook at home more often and ask for a huge meal-planning database with hundreds of recipes, pantry inventory, expiry dates, ratings, nutrition, prices, and dashboards.

The database may be useful, but the real end is simpler: **make dinner easy enough that you cook when you are tired**.

Intent Steward keeps the larger idea available while first identifying the smallest useful loop that could change dinner. If the database later proves useful, build it. If substantial research or tooling genuinely helps the decision, do that work rather than simplifying it away.

## Recommended Codex setup

The recommended setup uses two small layers:

```text
AGENTS.md                 persistent intent-first execution rule
    +
intent-steward/SKILL.md   detailed reasoning method
```

### 1. Install the skill

Copy [`skills/intent-steward`](skills/intent-steward) into your project at:

```text
.agents/skills/intent-steward
```

### 2. Add the companion instruction

Add [`templates/agents-snippet.md`](templates/agents-snippet.md) to the relevant `AGENTS.md` in your project.

The `AGENTS.md` layer improved consistency in our smoke tests, but it is **not required** for Intent Steward to function.

### 3. Use Codex normally

Implicit use is the intended everyday experience: Codex can select the skill when a task calls for it.

When you particularly want intent-first reasoning, invoke it explicitly:

```text
$intent-steward

<your request>
```

Explicit invocation has been the most consistently controlled mode in testing.

## What it changes

Intent Steward distinguishes:

- **Stated intent** — what you explicitly asked for.
- **Inferred intent** — what the request appears to be in service of.
- **Proposed intent** — a potentially better framing the agent may suggest.

A proposed intent must never silently replace what you asked for.

It also watches for:

- **Means–ends inversion** — the method becomes the goal.
- **Question drift** — the work becomes increasingly sophisticated while answering a different question from the one that mattered.

For trivial tasks it should stay out of the way. For musings, it should treat the thought as evidence about intent rather than automatically turning it into a project.

## Evidence and status

The current implementation is a release candidate for natural-use testing. Controlled behavioral smoke tests support the two-layer setup as a **consistency improvement**, not as a strict technical requirement.

See [`EVALUATION.md`](EVALUATION.md) for the concise findings. The historical v0.1–v0.6 names refer to evaluation rounds, not product versions.

No statistically significant benchmark claim is intended.

## Status

**`0.2.0-rc1`** — release candidate for real-world testing.

The project is intentionally small. The goal is better collaboration, not a larger intent-management framework.

## License

MIT
