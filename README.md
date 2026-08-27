# Intent Steward

**Help AI understand why you're asking, not just what you asked it to do.**

> **Infer → Expose → Refine → Act → Re-evaluate**

LLMs are very good at doing things: researching, writing, planning, comparing, coding, summarizing, and creating.

But what we ask an LLM to do is often only a **means** to something we actually care about.

Intent Steward helps keep that connection intact.

## A simple example

You say:

> "I keep forgetting important things. Make me a detailed productivity system."

A normal assistant might immediately build a large planner, tagging system, dashboard, and routine.

But the real goal may simply be:

> **Reliably remember and finish the important things.**

Intent Steward encourages the AI to notice that distinction, make it visible when useful, and keep the system serving the goal instead of becoming the goal.

| | Intent |
|---|---|
| **Stated** | Make me a detailed productivity system |
| **Inferred** | Help me reliably remember and finish important things |
| **Proposed** | Start with the simplest system that achieves that goal |

It should not repeatedly ask you to explain your intent before helping. The default is **infer first, expose the working interpretation, let you refine it, and continue**.

## More everyday examples

- **"Research 20 laptops for me."** → The goal may be choosing one laptop with enough confidence, not maximizing research.
- **"Build me a detailed budget spreadsheet."** → The goal may be understanding where money goes and avoiding running short.
- **"Plan every hour of my trip."** → The goal may be enjoying the trip without missing the experiences that matter.
- **"Summarize every email I receive."** → The goal may be noticing what needs attention without reading everything.
- **"Track every health metric."** → The goal may be healthier behavior, not becoming excellent at collecting health data.

The requested work may still be useful. Intent Steward is not anti-research, anti-tools, or anti-detail.

The principle is simple:

> **Use machinery when it serves the end. Reduce it when it has become detached from the end.**

## Recommended Codex setup

The current release candidate uses two small layers:

```text
AGENTS.md                 persistent intent-first execution rule
    +
intent-steward/SKILL.md   detailed reasoning method
```

### 1. Install the skill

Copy:

```text
skills/intent-steward/
```

into your project as:

```text
.agents/skills/intent-steward/
```

### 2. Add the small `AGENTS.md` companion

Copy `templates/agents-snippet.md` into the relevant `AGENTS.md` for your project.

The companion rule asks Codex to keep substantial research, tool use, artifact generation, and multi-step work connected to the decision or outcome they are meant to serve.

The skill can work without this layer. In our smoke tests, however, the small persistent instruction made implicit behavior more consistently resemble explicit Intent Steward behavior. Treat it as the **recommended default for consistency**, not a strict requirement.

### 3. Use Codex normally

Implicit use is the intended everyday experience. Codex can select the skill when it is relevant.

When you particularly want intent-first reasoning, explicitly invoke:

```text
$intent-steward
```

Explicit invocation has been the most consistent mode in testing.

## What Intent Steward does

### Infer

What is this request probably in service of?

### Expose

When it changes the approach, briefly surface the working interpretation rather than silently rewriting the user's goal.

### Refine

Let corrections and new evidence update that interpretation without forcing a long clarification interview.

### Act

Choose machinery that serves the intent. Before substantial research, tools, artifacts, or implementation, check whether they can still materially improve the underlying decision or outcome.

### Re-evaluate

Watch for two common failure modes:

- **Means–ends inversion** — the method becomes the goal.
- **Question drift** — the work becomes increasingly sophisticated while answering a different question from the one that mattered.

## Three kinds of intent

- **Stated intent** — what the user explicitly asks for.
- **Inferred intent** — what the agent believes the request is in service of.
- **Proposed intent** — a potentially more useful framing suggested by the agent.

A proposed intent must never silently replace the user's stated intent. The agent is a steward of intent, not its owner.

## Musings are not automatically tasks

If a user says:

> "I've noticed..."
>
> "I've been wondering..."
>
> "Maybe..."

that can be evidence about an underlying question rather than an instruction to immediately build something.

Intent Steward should help surface the question hiding inside the musing without turning every thought into a project.

## Evaluation so far

Intent Steward has gone through a series of controlled behavioral smoke tests in Codex using fresh conversations and matched model/reasoning settings.

What the tests support so far:

- **Trivial negative controls passed.** The skill stayed out of the way on simple tasks.
- **Explicit invocation has been consistently strong.** It often reduced unnecessary machinery while preserving useful analysis when the machinery genuinely served the decision.
- **Implicit discovery works.** Codex can recognize when the skill is relevant.
- **Discovery and adherence are different problems.** Earlier research-pressure tests showed cases where Codex loaded the skill and correctly described the underlying intent, but still continued excessive research.
- **The pre-machinery gate improved behavior.** Later tests showed the intent changing what the agent actually did, not just what it said.
- **The small `AGENTS.md` layer showed directional consistency gains.** In two authority/adherence tests, ambient use with the persistent instruction resembled explicit invocation more closely than skill-only implicit use did.
- **The clean stopping-boundary test passed for all skill conditions.** Baseline understood the user's real goal but still launched external research; explicit, implicit, and ambient Intent Steward all stopped before unnecessary engineering research.

These are controlled smoke tests, not a large benchmark. They support the current design as a useful release candidate, but do not establish statistical significance or prove that the `AGENTS.md` companion is strictly necessary.

The next phase is real-world use: does Intent Steward make normal LLM collaboration feel better without becoming another layer of process?

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
└── evals/
```

For projects where intent should persist over time, `templates/INTENT.md` is an optional project-level working model. It is useful for longer investigations, but is not required for ordinary use.

## Status

**0.2.0-rc1** — release candidate for real-world testing.

The project is intentionally small. The goal is better collaboration, not a larger intent-management framework.

## License

MIT
