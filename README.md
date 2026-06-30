# Shipwright

> Claude Code skills for writing the spec docs your agents read — so they build what you meant, not what they guessed.

An autonomous agent doesn't stop when its context runs thin. It fills the gap with a plausible guess and builds on it at full speed — and you find out only after it's built the wrong thing well. Shipwright is a toolbox of skills for writing the docs that hold the context the agent is missing: a spec, your conventions, a task brief. Each one drafts the whole document first, then asks you only the decisions that actually matter.

<!--
SEE IT WORK — replace this block with a real demo.
Best: a short GIF or screencast of one skill firing in Claude Code and producing
a doc. Second best: a before/after transcript — the thin prompt that sends an
agent down the wrong path, then the same task after a Shipwright doc gives it the
context. Show it doing the work; don't describe it.
-->

## Install

In Claude Code, register the marketplace and install the plugin:

```
/plugin marketplace add TeddyRoosevelty/Shipwright-Marketplace
/plugin install spec-docs@shipwright
```

Or run `/plugin` to browse and install from the menu.

To confirm it worked, ask Claude to "write our JTBD" — the jtbd skill should pick it up.

## Why it works this way

- **Draft first, then ask only what matters.** Most doc tools interrogate you up front with a wall of questions. These skills draft the whole document from what's already in the repo and the conversation, then surface only the decisions a guess would get wrong. You review and correct instead of dictating from scratch.
- **Written to be read by agents, not filed by humans.** The output is the context an agent loads before it builds — structured so a cold agent can act on it, not a document that rots in a folder.
- **A toolbox, not a methodology.** Reach for the doc that fits the gap you're feeling and leave the rest. Nothing assumes you ran the skill before it, and nothing makes you run the one after.

## Skills

### Direction

| Skill | What it does | Trigger it with |
|-------|--------------|-----------------|
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

## What it doesn't do

- **It doesn't verify what the agent builds.** Shipwright is the context going *in*. Checking that the understanding survived the build — review, verification — is a different job, and not this one.
- **It doesn't enforce a process.** No skill requires another. There's no flow to follow and nothing tracks whether you wrote the "right" docs.
- **It doesn't replace your judgment.** It drafts and narrows the decisions; you still make the calls that matter.

## License

MIT — see [LICENSE](LICENSE).
