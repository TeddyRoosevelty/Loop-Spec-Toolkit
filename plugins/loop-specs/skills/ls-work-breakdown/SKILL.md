---
description: Design a work breakdown — a body of work decomposed into discrete tasks, ordered by dependency and sized, so it can be parceled out and tracked. Use when the user wants the task tree and sequence for a large effort — "break this down", "what are the tasks for X" — rather than a build plan's per-task technical approach.
argument-hint: "[the body of work to break down — or a path to its plan or requirements doc]"
---

# Work Breakdown Designer

Draft and refine a work breakdown with the user — a body of work decomposed into discrete, trackable tasks, ordered by dependency. Decompose the whole work with no gaps, and get the dependencies right so the sequence actually works.

## Process

Read [assets/work-breakdown-template.md](assets/work-breakdown-template.md) up front — it's the artifact every step builds toward. Compress a step the work doesn't earn — acknowledge the skip rather than dropping it silently.

### 1. Ground in the work

Read the plan or requirements doc if one was pointed to, and any existing breakdown. Settle what's being decomposed and its scope, then recap before breaking it down.

### 2. Analyze

Break the work into its real pieces. Decompose it into discrete tasks at a trackable grain — covering the whole work with no gaps — and find the dependencies between them: what must come before what. Read the code for the natural seams the breakdown should follow.

Scale the method to the effort: read directly for a small one; for a large one touching many areas, dispatch parallel search agents to map them, then verify yourself. Test the result against the work breakdown standards below before drafting.

### 3. Propose

Shape the decomposition into a draft, then check it holds.

#### Produce the draft

Fill the template from the analysis: the overview, the tasks grouped where there's structure, and the dependencies and sequence. Add the sizing or phases sections when they help parcel the work, and keep sizing rough — relative, not hours.

#### Validate

Check that the decomposition covers the whole work with no gaps, each task is discrete and trackable, and the dependency ordering actually works — nothing sequenced before what it needs.

### 4. Present

Present the draft so the reader can follow it without the code in front of them.

#### The draft

Present the breakdown — the best-effort decomposition from what you found. It's both the first draft and the thing the user reacts to.

#### Honest account

Close with an honest read: where the breakdown is complete and grounded, where a task is still too big to track, and any dependency you're unsure of.

### 5. Facilitate

Surface the decisions that actually matter — the ones your analysis exposed. Use the draft as something concrete to push against, but draw the questions from the work's real structure.

Be a thinking partner with small batches of questions, considering what the user leans toward before offering your read. Useful angles:

- Whether the decomposition has gaps, or a task hides several.
- Whether the sequence respects the real dependencies.
- Where tasks could run in parallel, against where they must be serial.

The result can re-affirm the draft, reshape it, or re-decompose the work. When the structure reframes, rework the breakdown as a v2 and present it as such. Before capturing, reflect the settled shape back — the tasks, the sequence, and anything you'd flag. If the user revises, fold it in and re-confirm rather than writing straight away.

### 6. Capture

Save only when the user asks or confirms. Ask what's next with the blocking-question tool:

- **Refine in conversation (or stop here)** — no file written; the alignment carries forward in conversation.
- **Save** — write the breakdown per the template and the plugin data location config below.

## Work breakdown standards

The bar a work breakdown clears. A strong breakdown is:

- **Complete** — the decomposition covers the whole work, with no gaps and no overlap.
- **Discrete** — each task is a distinct, trackable piece, not a vague theme.
- **Right-grained** — tasks are small enough to track and large enough to matter, not micro-steps.
- **Dependency-correct** — the ordering works; nothing is sequenced before what it depends on.
- **Grounded** — the breakdown follows the work's real seams, not an arbitrary split.

## Running autonomously

When asked to run autonomously, skip facilitation.

Instead, run the "Verify on request" step.

## Verify on request

When asked to verify the breakdown.

Dispatch an adversarial agent to review the draft, briefed to stress-test the breakdown; to find where its decomposition and dependency ordering don't hold by walking through it.
- Don't bias on the results, tell it what to look for, or guess what it'll find.
- Request it to provide only confirmed, valuable findings over minor or unconfirmed ones. No findings are better than wrong ones.

Review and assess the results provided by the agent. Verify each finding it raises. They could be wrong or misled. Incorporate only what is valid and adds value (even if minor enhancements).

## Plugin Data Location Config

Unless specified otherwise, use the plugin data for where to find and save relevant plugin artifacts.
- **Plugin Data Path** — `${user_config.save_path}`, or `.loop-specs` if `save_path` isn't set. Create it if needed.
- **Feature folder** — `<plugin-data-path>/<feature-slug>`.
- **Feature slug** — 2–4 words, hyphenated. Before saving, check the existing folders under the plugin data path for any that clearly match (name and recency). Assume a new slug if none clearly match.
- **Save File Name** — `<feature-folder>/work-breakdown.md`. Fixed, lowercase.

Unsure where it should go? Ask with the blocking-question tool (unless running autonomously). Otherwise assume the defaults and confirm the resolved path in the close.

## Writing style

- Write the breakdown and everything in chat to prioritize the reader's understanding — plain language, no jargon beyond the domain terms the work genuinely needs.
- Don't narrate the context-gathering or your analysis as a frame; use it to shape the breakdown.
- Explain what isn't obvious — the reader isn't looking at the code or your analysis.
- Keep questions for the user in their own section — don't bury them in prose.
- Reserve the blocking-question tool for mechanical decisions with clear answers; framing and judgment belong in conversation.


## Argument Flags
If the user arguments includes any of the following flags, follow them as if they are additional instructions:
--save, --autoSave: Once finalized, save the document in the save set without prompting
--autonomous, --auto: Run in autonomous mode. (see: "Running autonomously")
--verify: Run the "Verify on request" step.
