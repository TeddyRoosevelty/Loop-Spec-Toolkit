# Shipwright

> A toolbox of Claude Code skills for writing the spec docs your agents read.

Autonomous agents act on whatever context they have. When that context is thin, an agent doesn't stop to ask — it fills the gap with a guess and builds on it at full speed. These skills help you write the docs that hold that missing context — a spec, a decision record, conventions, a brief. Each drafts the whole thing first, then asks you only the decisions that actually matter.

<todo>
Demo — a GIF, screenshot, or short before/after transcript of a skill actually
firing in Claude Code. Show it doing real work; don't describe it.
</todo>

## Install

In Claude Code, register the marketplace and install the plugin:

```
/plugin marketplace add TeddyRoosevelty/Shipwright-Marketplace
/plugin install spec-docs@shipwright
```

Or run `/plugin` to browse and install from the menu.

To confirm it worked, ask Claude to "write our strategy" — the strategy skill should pick it up.

## Skills

A toolbox, not a methodology: reach for the doc that fits the gap you're feeling, and leave the rest.

### Direction

| Skill | What it does | Trigger it with |
|-------|--------------|-----------------|
| strategy | Maintains STRATEGY.md — the target problem, approach, users, metrics, and tracks of work. | "write our strategy", "update the roadmap" |
| jtbd | Captures the main job a product is hired for, its success criteria, and the scenarios it serves. | "write our JTBD", "map the user scenarios" |
| problem-statement | Pins down the specific problem worth solving, with evidence, before any solution. | "what problem are we really solving", "write up this problem" |
| requirements | Turns a raw idea into a requirements doc by exploring interpretations and refining to one. | "explore this idea", "what are different ways to do this" |
| ideation | Surveys a repo or focus for its strongest problems and returns a shortlist of ideas. | "find ideas to improve X", "what's worth doing here" |

### Design

| Skill | What it does | Trigger it with |
|-------|--------------|-----------------|
| architecture | Maps a system's components, how they fit, the load-bearing decisions, and the stack. | "document the architecture", "map how this fits together" |
| tech-spec | Drafts a reviewable design (RFC) for one piece of work — approach, alternatives, open questions. | "write a design doc for X", "draft an RFC" |
| api-contract | Pins down an interface — operations, request/response shapes, errors, and auth consumers build against. | "spec this API", "define the contract for X" |
| data-model | Captures the entities a system holds, their fields, relationships, and the rules over the data. | "document the data model", "design the schema for X" |
| nfr | Turns quality bars — performance, reliability, security, accessibility — into measurable targets. | "what are our performance targets", "write the NFRs for X" |

### Shared foundations

| Skill | What it does | Trigger it with |
|-------|--------------|-----------------|
| glossary | Defines the domain terms a project uses, so people and agents use words consistently. | "write our glossary", "define the domain terms" |
| conventions | Captures the repo-wide rules a cold agent must follow — structure, commands, patterns. | "capture our conventions", "write the build rules for this repo" |
| decision-record | Records one significant decision (ADR) — context, alternatives, choice, consequences — so it isn't re-litigated. | "record this decision", "write an ADR for X" |

### Delivery

| Skill | What it does | Trigger it with |
|-------|--------------|-----------------|
| work-breakdown | Decomposes a body of work into discrete tasks, ordered by dependency and sized. | "break this down", "what are the tasks for X" |
| task-brief | Packages one unit of work for a cold agent — task, context, files, constraints, verification. | "write a task brief for X", "package this task for an agent" |

### Risk & quality

| Skill | What it does | Trigger it with |
|-------|--------------|-----------------|
| assumptions | Surfaces the beliefs a piece of work rests on, each rated for risk with a way to validate it. | "what are we assuming here", "list the assumptions behind X" |
| risk-register | Tracks the risks facing a body of work, each with likelihood, impact, and response. | "what are the risks", "build a risk register for X" |
| threat-model | Maps what's worth protecting, how it could be attacked, and the mitigations that defend it. | "threat-model this", "what are the security risks for X" |
| test-strategy | Plans what to test, at which levels, and how much coverage is enough — risk-driven. | "how should we test this", "write a test strategy for X" |
| qa-plan | Lists the concrete pre-ship checks and the exit gate that says it's ready. | "what should we check before shipping X", "write the QA plan" |

## License

MIT — see [LICENSE](LICENSE).
