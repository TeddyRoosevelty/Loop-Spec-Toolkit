# Loop Spec Toolkit

> The easiest way to turn your vision and judgment into specs for Claude Code loops, goals, and autonomous work.

An opinionated collection of skills for creating specs, built to prioritize your time, focus, and effort to get the most out of your sessions.

- **Low manual effort** - right sized to where it matters
- **Right sized** - high impact specs, leveraging best practices
- **Flexible execution** - to fit different tasks, sizes, and personal workflows

Good context and requirements allow autonomous tasks to deliver what you want and expect - defining them shouldn't be the hardest part.

*See [Specs within Loop Engineering](docs/specs-within-loop-engineering.md).*

## Usage Example

Building a task-management board backend:

```bash
# 1. Shape the specs that matter most for the task - interactive working sessions; review each doc as you go. 
/ls-requirements "Write the requirements for our task management board backend."
/ls-architecture "I have an idea for the architecture I'd like..."

# 2. Automatically pre-plan the specs you want to see and/or refine
/ls-api-contract "Design the api for my review --autonomous --autoSave"
/ls-test-strategy "let's create tests --autonomous --autoSave"

# 3. When ready, hand them to a loop. The agent will naturally decide themselves for anything not specified.
/goal "@.loop-specs/task-management-backend implement this backend completely. Before stopping, make sure all requirements are complete, the build, tests, and linter are all green."
```

**Output**: The spec skills leave a reviewable bundle on disk:

```
.loop-specs/
└── task-management-backend/
    ├── requirements.md
    ├── architecture.md
    ├── api-contract.md
    └── test-strategy.md
```

*Create as many or as few targetted specs as you need. Choose based on your task and your priorities.*

*Each helps with surfacing and guiding the model's judgement and thinking ahead of execution. They provide a targetted, focused way to help manage the context, requirements, and direction for the task.*

## How it works

Each spec you build for a feature gets added to a small feature bundle - each one focused on a specific angle of the work. Together, the bundle is the context you're handing the loop: made explicit and reviewable, instead of trapped in your head.

### What each doc gives you

Every skill owns one question and answers it using a well-designed template that reflects best practice. Keeping them separate means the model spends focused effort on that single high-leverage angle, so each doc stays right-sized and earns its place. Together they cover a task from the surfaces you choose to pre-define.

### How each skill works

Every skill runs the same shape - a short, collaborative process, not a one-shot generator:

- **Analyze** - reads your inputs and code, recaps what it understood to confirm direction, then works it into a grounded read (dispatching subagents when the task needs it).
- **Draft** - produces the spec and checks its own work, then presents it with an assessment of what rests on assumptions and the core judgement areas.
- **Facilitate** - works through the decisions that actually matter with you, converging on a version you approve.
- **Save** - writes the doc once aligned/confirmed.

Need it hands-off? Any skill can also run autonomously - it skips the back-and-forth and self-checks before saving. Check and refine it after, as needed.

### Mixing and matching

Pick the few docs that matter for the task and its size - one requirements doc for something small, a fuller set when the work would benefit from it. Since the outputs are light, standard artifacts, the bundle drops into a one-shot task, a loop, a goal, or a long-running workflow.

## Install

### Claude Code

From inside Claude Code, add the marketplace and install the plugin:

```
/plugin marketplace add TeddyRoosevelty/Loop-Spec-Toolkit
/plugin install loop-specs@loop-spec-toolkit
```

Verify it worked by running `/plugin` - `loop-specs` should appear in your installed plugins. The skills are then available automatically; just describe what you want (e.g. *"write our JTBD"*) and the matching skill kicks in.

Generated docs are saved under `.loop-specs/` in your project by default, grouped into a subfolder per feature.

### Codex or other harnesses

Just point your agent to the repo. They're smart, they'll figure it.

## Skills

Each of these is a spec - a goal to satisfy or a constraint to check against. They differ by what they pin down.

### Purpose - what to build and the bar it must clear


| Skill               | What it does                                                                                                                    | Trigger it with                                                |
| ------------------- | ------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------- |
| **ls-jtbd**         | Defines the job a product is hired for, the criteria users judge it by, and the scenarios it should serve.                      | *"write our JTBD"*, *"map the user scenarios"*                 |
| **ls-requirements** | Turns a raw idea into a requirements doc by exploring genuinely different interpretations, then refining to a chosen direction. | *"explore this idea"*, *"what are different ways to do this"*  |
| **ls-nfr**          | Turns quality bars (performance, reliability, security, accessibility) into measurable, verifiable targets.                     | *"write the NFRs for X"*, *"what are our performance targets"* |


### Design - how the system is shaped


| Skill               | What it does                                                                                                    | Trigger it with                                               |
| ------------------- | --------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------- |
| **ls-architecture** | Maps a system's components, how they fit together, the load-bearing decisions, and the stack.                   | *"document the architecture"*, *"map how this fits together"* |
| **ls-tech-spec**    | Drafts the design (RFC) for one piece of work: approach, components, alternatives weighed, and open questions.  | *"write a design doc for X"*, *"draft an RFC"*                |
| **ls-api-contract** | Pins down an interface contract - operations, request/response shapes, errors, and auth - grounded in the code. | *"spec this API"*, *"define the contract for X"*              |
| **ls-data-model**   | Captures the entities a system holds, their fields and relationships, and the rules that govern the data.       | *"document the data model"*, *"design the schema for X"*      |


### Standards - the language and rules work must conform to


| Skill              | What it does                                                                                       | Trigger it with                                                      |
| ------------------ | -------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------- |
| **ls-conventions** | Extracts the repo-wide rules a cold agent must follow to produce work that fits the project.       | *"capture our conventions"*, *"write the build rules for this repo"* |
| **ls-glossary**    | Captures the domain terms a project uses and their precise definitions, for consistent vocabulary. | *"write our glossary"*, *"define the domain terms"*                  |


### Plan of work - how the effort is sliced and handed off


| Skill                 | What it does                                                                                 | Trigger it with                                                  |
| --------------------- | -------------------------------------------------------------------------------------------- | ---------------------------------------------------------------- |
| **ls-work-breakdown** | Decomposes a large effort into discrete tasks, ordered by dependency and sized.              | *"break this down"*, *"what are the tasks for X"*                |
| **ls-task-brief**     | Packages one unit of work into a self-contained brief a cold agent can build without asking. | *"write a task brief for X"*, *"package this task for an agent"* |


### Risk & proof - what could go wrong and how you'll know it's right


| Skill                | What it does                                                                                               | Trigger it with                                                   |
| -------------------- | ---------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------- |
| **ls-assumptions**   | Surfaces the beliefs and bets a piece of work rests on, each rated for risk with a way to validate it.     | *"what are we assuming here"*                                     |
| **ls-risk-register** | Surfaces and tracks what could derail a body of work, each risk with likelihood, impact, and response.     | *"what are the risks"*, *"build a risk register for X"*           |
| **ls-threat-model**  | Analyzes what's worth protecting, how it could be attacked, and the mitigations that defend it.            | *"threat-model this"*                                             |
| **ls-test-strategy** | Plans how to prove a body of work correct: what to test, at which levels, and how much coverage is enough. | *"how should we test this"*                                       |
| **ls-qa-plan**       | Builds a runnable pre-release checklist - automated, manual, and exploratory checks - with the exit gate.  | *"write the QA plan"*, *"what should we check before shipping X"* |


## Plugin Roadmap

Loop Spec Toolkit is becoming a family of plugins around one core principle: Creating specs for loops, goals, and autonomous work should be easy, flexible, and right-sized. 

- ✅ **Loop Specs** — a plugin with one skill per spec template; Each its own call giving the most control.
- ⚒ **Loop Spec Skill** *(unified)* — a single skill entry point; routes to the right spec(s) providing a smaller skill footprint.
- ◻ **Loop Spec Workflow** — Claude Code workflow/ultracode templates, for more customization and leverage.
- ◻ **Loop Spec Evals** — the tests a loop is judged by: deterministic checks and LLM-judgement rubrics for goals and loops.

## License

MIT - see [LICENSE](LICENSE).