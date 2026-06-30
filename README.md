# Loop Spec Toolkit

> The easiest way to turn your vision and judgment into requirements for Claude Code loops, goals, and autonomous work.

An opinionated toolkit of skills built to prioritize:

- **Low manual effort** — minimal hand-authoring
- **High-impact specs** — requirements that actually steer the agent
- **Flexible execution** — fits loops, goals, and autonomous runs

Good requirements are what make autonomous tasks deliver what you actually expect — and defining them shouldn't be the hardest part of the job.

<todo>
Demo — a GIF, screenshot, or short before/after transcript of a skill actually
firing in Claude Code. Show it doing real work; don't describe it.
</todo>

## Install

From inside Claude Code, add the marketplace and install the plugin:

```
/plugin marketplace add TeddyRoosevelty/Loop-Spec-Toolkit
/plugin install loop-specs@loop-spec-toolkit
```

Verify it worked by running `/plugin` — `loop-specs` should appear in your installed plugins. The skills are then available automatically; just describe what you want (e.g. *"write our JTBD"*) and the matching skill kicks in.

Generated docs are saved under `.loop-specs/` in your project by default, grouped into a subfolder per feature.

## Skills

Each of these is a spec — a goal to satisfy or a constraint to check against. They differ by what they pin down.

### Purpose — what to build and the bar it must clear

| Skill | What it does | Trigger it with |
|-------|--------------|-----------------|
| **jtbd** | Defines the job a product is hired for, the criteria users judge it by, and the scenarios it should serve. | *"write our JTBD"*, *"map the user scenarios"* |
| **requirements** | Turns a raw idea into a requirements doc by exploring genuinely different interpretations, then refining to a chosen direction. | *"explore this idea"*, *"what are different ways to do this"* |
| **nfr** | Turns quality bars (performance, reliability, security, accessibility) into measurable, verifiable targets. | *"write the NFRs for X"*, *"what are our performance targets"* |

### Design — how the system is shaped

| Skill | What it does | Trigger it with |
|-------|--------------|-----------------|
| **architecture** | Maps a system's components, how they fit together, the load-bearing decisions, and the stack. | *"document the architecture"*, *"map how this fits together"* |
| **tech-spec** | Drafts the design (RFC) for one piece of work: approach, components, alternatives weighed, and open questions. | *"write a design doc for X"*, *"draft an RFC"* |
| **api-contract** | Pins down an interface contract — operations, request/response shapes, errors, and auth — grounded in the code. | *"spec this API"*, *"define the contract for X"* |
| **data-model** | Captures the entities a system holds, their fields and relationships, and the rules that govern the data. | *"document the data model"*, *"design the schema for X"* |

### Standards — the language and rules work must conform to

| Skill | What it does | Trigger it with |
|-------|--------------|-----------------|
| **conventions** | Extracts the repo-wide rules a cold agent must follow to produce work that fits the project. | *"capture our conventions"*, *"write the build rules for this repo"* |
| **glossary** | Captures the domain terms a project uses and their precise definitions, for consistent vocabulary. | *"write our glossary"*, *"define the domain terms"* |

### Plan of work — how the effort is sliced and handed off

| Skill | What it does | Trigger it with |
|-------|--------------|-----------------|
| **work-breakdown** | Decomposes a large effort into discrete tasks, ordered by dependency and sized. | *"break this down"*, *"what are the tasks for X"* |
| **task-brief** | Packages one unit of work into a self-contained brief a cold agent can build without asking. | *"write a task brief for X"*, *"package this task for an agent"* |

### Risk & proof — what could go wrong and how you'll know it's right

| Skill | What it does | Trigger it with |
|-------|--------------|-----------------|
| **assumptions** | Surfaces the beliefs and bets a piece of work rests on, each rated for risk with a way to validate it. | *"what are we assuming here"* |
| **risk-register** | Surfaces and tracks what could derail a body of work, each risk with likelihood, impact, and response. | *"what are the risks"*, *"build a risk register for X"* |
| **threat-model** | Analyzes what's worth protecting, how it could be attacked, and the mitigations that defend it. | *"threat-model this"* |
| **test-strategy** | Plans how to prove a body of work correct: what to test, at which levels, and how much coverage is enough. | *"how should we test this"* |
| **qa-plan** | Builds a runnable pre-release checklist — automated, manual, and exploratory checks — with the exit gate. | *"write the QA plan"*, *"what should we check before shipping X"* |

## License

<todo>
One line naming the license + a LICENSE file in the repo.
</todo>
