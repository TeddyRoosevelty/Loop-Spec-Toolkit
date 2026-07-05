# Task Brief — spec card

The self-contained packet a cold agent reads to build one unit of work without asking: the task and scope, the context it needs, where to work, the constraints to follow, and how to verify it's done. Say what to build and how to confirm it, not the implementation. A brief covers one unit a cold agent can execute on its own; if the work is larger, narrow to one unit or say so.

**Template:** [../templates/task-brief.md](../templates/task-brief.md) · **Saves as:** `task-brief.md`

## Ground in

The plan or requirements doc if one exists, and any existing brief. Settle the one unit being briefed and its boundary.

## Analysis method

Work out what a cold agent needs to build this without asking:

- **Fix who reads it.** A capable engineer who knows the language and framework and can read the repo's own conventions — but knows nothing about *this* task, *this* plan, or the conversation behind it. Task-specific knowledge goes in the brief; general competence stays out.
- **Ground in the code.** Read the files, patterns, and conventions the work touches — enough to name where to start and what to follow.
- **Settle the brief's five pieces.** The task and its scope, the context that bears on it, the starting points, the constraints to follow, and what "done and correct" looks like.
- **Get the two load-bearing ones right.** Context — enough to build it right, not a tour. Acceptance — checks the agent can run itself, not a bar only a human could judge.

## Drafting notes

Fill the task and scope, the context, the starting points, the constraints and conventions, and the acceptance and verification. Add the prerequisites section only when something must be in place first. Validate that the files are named, the constraints are stated, the acceptance is self-checkable, and the brief doesn't smuggle in the implementation. The strongest check is a cold read: simulate the build on paper from the brief alone, and fix every point where the builder would have to ask, guess, or couldn't self-check "done."

## Facilitation angles

- Whether the scope is one unit a cold agent could land in one go.
- Where the context is too thin to build right, or too thick to be useful.
- Whether the acceptance is something the agent can verify on its own.

## Standards

- **Self-contained** — a cold agent could build it from the brief alone, without asking or guessing.
- **Scoped to one unit** — it covers a single, bounded piece of work, not a whole body of it.
- **Grounded** — it names the real files, patterns, and conventions the work touches.
- **Verifiable** — the acceptance is something a cold agent can self-check, and the verification names how.
- **Not pre-written** — it says what to build and how to confirm it, leaving the implementation to the build.

## Verify focus

A cold read: give the verifying agent *only* the brief — no extra context, no hint at what's thin — and have it simulate the build on paper, returning every point where it would have to ask, guess, or couldn't self-check "done." Only gaps that would genuinely block or mislead the build.
