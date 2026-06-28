---
description: Design a task brief — the self-contained packet a cold agent reads to build one unit of work without asking: the task, context, files, constraints, and how to verify it's done. Use when the user wants to hand one unit to an unsupervised agent — "write a task brief for X", "package this task for an agent" — rather than plan the whole body of work.
argument-hint: "[the unit of work to brief — or a path to its plan or requirements doc]"
---

# Task Brief Designer

Draft and refine a task brief with the user — the self-contained packet a cold agent reads to build one unit of work without asking: the task and scope, the context it needs, where to work, the constraints to follow, and how to verify it's done. Say what to build and how to confirm it, not the implementation.

## Process

Read [assets/task-brief-template.md](assets/task-brief-template.md) up front — it's the artifact every step builds toward. Compress a step the work doesn't earn — acknowledge the skip rather than dropping it silently.

### 1. Ground in the work

Read the plan or requirements doc if one was pointed to, and any existing brief. Settle the one unit being briefed and its boundary, then recap before drafting. A task brief covers one unit a cold agent can execute on its own; if the work is larger, narrow to one unit or say so.

### 2. Analyze

Work out what a cold agent needs to build this without asking.

- **Fix who reads it.** A capable engineer who knows the language and framework and can read the repo's own conventions — but knows nothing about *this* task, *this* plan, or the conversation behind it. Task-specific knowledge goes in the brief; general competence stays out.
- **Ground in the code.** Read the files, patterns, and conventions the work touches — enough to name where to start and what to follow.
- **Settle the brief's five pieces.** The task and its scope, the context that bears on it, the starting points, the constraints to follow, and what "done and correct" looks like.
- **Get the two load-bearing ones right.** Context — enough to build it right, not a tour. Acceptance — checks the agent can run itself, not a bar only a human could judge.

Test the result against the task brief standards below before drafting.

### 3. Propose

Shape the analysis into a draft, then check it holds.

#### Produce the draft

Fill the template from the analysis: the task and scope, the context, the starting points, the constraints and conventions, and the acceptance and verification. Say what to build and how to verify it, not the code. Add the prerequisites section only when something must be in place first.

#### Validate

**Confirm** that the files are named, the constraints are stated, the acceptance is self-checkable, and the brief doesn't smuggle in the implementation.

**Perform a code read review** - Dispatch a fresh agent given *only* the brief and have it simulate the build on paper: return every point where it would have to ask, guess, or couldn't self-check "done." 

- Verify the results and assessment of the code read — incorporating any valid gaps into the brief. What you don't fix, share into the readout. For a brief small enough that the work doesn't earn the dispatch, run the cold read in session and say so.

### 4. Present

Present the draft so the reader can follow it without the code in front of them.

#### The draft

Present the brief — the best-effort packet from what you found. It's both the first draft and the thing the user reacts to.

#### Honest account

Close with an honest read: where the brief is self-contained, where a gap might force the agent to guess, and what it assumes is already in place.

### 5. Facilitate

Surface the decisions that actually matter — the ones your analysis exposed. Use the draft as something concrete to push against, but draw the questions from what a cold agent would need.

Be a thinking partner with small batches of questions, considering what the user leans toward before offering your read. Useful angles:

- Whether the scope is one unit a cold agent could land in one go.
- Where the context is too thin to build right, or too thick to be useful.
- Whether the acceptance is something the agent can verify on its own.

The result can re-affirm the draft, reshape it, or re-scope the unit. When the scope reframes, rework the brief as a v2 and present it as such. Before capturing, reflect the settled shape back — the task, the constraints, the acceptance, and anything you'd flag. If the user revises, fold it in and re-confirm rather than writing straight away.

### 6. Capture

Save only when the user asks or confirms. Ask what's next with the blocking-question tool:

- **Refine in conversation (or stop here)** — no file written; the alignment carries forward in conversation.
- **Save** — write the brief per the template and the plugin data location config below.

## Task brief standards

The bar a task brief clears. A strong brief is:

- **Self-contained** — a cold agent could build it from the brief alone, without asking or guessing.
- **Scoped to one unit** — it covers a single, bounded piece of work, not a whole body of it.
- **Grounded** — it names the real files, patterns, and conventions the work touches.
- **Verifiable** — the acceptance is something a cold agent can self-check, and the verification names how.
- **Not pre-written** — it says what to build and how to confirm it, leaving the implementation to the build.

## Running autonomously

When asked to run autonomously, skip facilitation.

Instead, run the "Verify on request" step.

## Verify on request

When asked to verify the brief.

Dispatch a fresh cold-read agent given *only* the brief, and have it simulate the build on paper — returning every point where it would have to ask, guess, or couldn't self-check "done."
- Give it only the brief — no extra context, and no hint at what you think is thin; what the brief alone conveys is the whole test.
- Have it report only the gaps that would genuinely block or mislead the build, over minor or unconfirmed ones. No gaps are better than wrong ones.

Review and assess the results provided by the agent. Verify each gap it raises — they could be wrong or misled — and fold only the valid ones into the brief, then re-present what changed. For a brief small enough that the work doesn't earn the dispatch, run the cold read in session and say so.

## Plugin Data Location Config

Unless specified otherwise, use the plugin data for where to find and save relevant plugin artifacts.
- **Plugin Data Path** — `${user_config.save_path}`, or `.spec-docs/docs` if `save_path` isn't set. Create it if needed.
- **Task briefs folder** — `<plugin-data-path>/task-briefs`.
- **Save File Name** — `<task-briefs-folder>/YYYY-MM-DD-<topic>-brief.md`
- **File name** — today's date and the topic.

Unsure where it should go? Ask with the blocking-question tool. Otherwise assume the defaults and confirm the path in the close.

## Writing style

- Write the brief and everything in chat to prioritize the reader's understanding — plain language, no jargon beyond the domain terms the work genuinely needs.
- Don't narrate the code-reading or your analysis as a frame; use it to shape the brief.
- Explain what isn't obvious — the agent reading the brief isn't looking at your analysis.
- Keep questions for the user in their own section — don't bury them in prose.
- Reserve the blocking-question tool for mechanical decisions with clear answers; framing and judgment belong in conversation.
