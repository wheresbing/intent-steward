# Intent Steward

**Help AI agents understand why you are asking, not just what you asked them to do.**

> Do not make users perfectly specify their intent before helping them. Help them discover it while doing the work.
>
> **Infer → Expose → Refine → Act → Re-evaluate**

LLMs are very good at doing things: researching, writing, planning, coding, comparing, summarizing, and creating.

But what we ask an LLM to do is often only a **means** to something we actually care about.

Intent Steward helps an agent keep that connection visible.

## A simple example

A user says:

> "I keep forgetting important things. Make me a detailed productivity system."

A typical assistant may immediately create a complicated planner, routine, tagging system, and dashboard.

But the real goal may simply be:

> **Reliably remember and finish the important things.**

Intent Steward might respond:

> "It sounds like the real goal is to reliably remember and finish important things. A detailed productivity system is one possible way to do that. I’ll start with the simplest setup that keeps the important things visible, and only add complexity if it helps."

Then it continues helping.

The important distinction is:

| | Intent |
|---|---|
| **Stated** | Make me a detailed productivity system |
| **Inferred** | Help me reliably remember and finish important things |
| **Proposed** | Start with the simplest system that achieves that goal |

The agent is not refusing the request or pretending it knows better. It is keeping the requested **means** connected to the underlying **end**.

## More everyday examples

- **"Research 20 laptops for me."** → The real goal may be to choose one laptop with enough confidence, not to maximize research.
- **"Build me a detailed budget spreadsheet."** → The real goal may be to understand where money is going and avoid running short.
- **"Plan every hour of my day."** → The real goal may be to make consistent progress on the few things that matter most.
- **"Summarize every email I receive."** → The real goal may be to notice what needs attention without reading everything.
- **"Create a huge itinerary for my trip."** → The real goal may be to enjoy the trip and cover the important experiences without being over-scheduled.

In each case, the requested task may still be useful. Intent Steward simply asks the agent to remember **why the task exists**.

## Core behavior

1. **Infer** the likely underlying intent from the user's request and context.
2. **Expose** that interpretation briefly when it affects the approach.
3. **Refine** it when the user corrects it or new evidence changes the picture.
4. **Act** on the next step that best serves the intent.
5. **Re-evaluate** when the work starts drifting away from its purpose.

The agent should not repeatedly ask:

> "What is your intent?"

When reasonable, it should infer a working interpretation, make it visible, and continue.

## Three kinds of intent

- **Stated intent** — what the user explicitly asks for.
- **Inferred intent** — what the agent believes the request is in service of.
- **Proposed intent** — a potentially more useful framing the agent suggests.

A proposed intent must never silently replace what the user actually asked for.

## Common failure modes

### Means–ends inversion

The method becomes the goal.

For example, someone starts by trying to remember important things, then spends weeks perfecting a productivity system instead of using it to remember important things.

### Question drift

The work gradually answers a different question from the one that mattered.

For example:

`Which laptop should I buy?`
→ `Which laptops have the best benchmark scores?`
→ `Which benchmark methodology is most accurate?`

The research may become impressive while no longer helping the person make the original decision.

### Clarification tax

The agent forces the user to explain everything before doing anything useful.

Intent Steward prefers:

> "My working interpretation is X. That suggests Y is the most useful next step."

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

The skill supports three simple modes:

- **FRAME** — what are we really trying to achieve?
- **ADVANCE** — what is the most useful thing to do next?
- **REVIEW** — are we still solving the right problem?

## Design principles

- Intent is a working hypothesis, not a contract.
- Infer before interrogating.
- Keep the means connected to the end.
- Suggest better framing without taking control away from the user.
- Prefer useful progress over unnecessary machinery.
- Ask: **"Why are we doing this next?"**
- Keep it lightweight for simple tasks.

## Status

Early draft / v0.1. The project is intentionally small so the behavior can be tested before adding more machinery.

## License

MIT
