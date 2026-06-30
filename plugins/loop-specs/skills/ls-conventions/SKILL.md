---
description: Design a conventions doc — the repo-wide rules a cold agent must follow to produce work that fits: structure, commands, coding patterns, and project-specific rules, extracted from the real code. Use when the user wants the build-context that keeps an agent's work consistent — "capture our conventions", "write the build rules for this repo" — rather than auditing an existing CLAUDE.md.
argument-hint: "[the repo to capture conventions for — defaults to the current repo]"
---

# Conventions Designer

Draft and refine a conventions doc with the user — the repo-wide rules a cold agent must follow to produce work that fits: what the project is and its stack, where things live, how to build and test, and the coding patterns and rules to follow. Extract the conventions the code actually follows, not generic best practice, and mark intended changes as intended.

## Process

Read [assets/conventions-template.md](assets/conventions-template.md) up front — it's the artifact every step builds toward. Compress a step the work doesn't earn — acknowledge the skip rather than dropping it silently.

### 1. Ground in the repo

Read any existing conventions doc, `CLAUDE.md`, or contributing docs, and the repo's config — package manifests, lint and format setup, CI. Recap what the project is and how it's organized, then confirm the scope before drafting.

### 2. Analyze

Extract the conventions the code actually follows. Read across the codebase for the structure, the build and test commands, and the patterns and idioms work follows — sampling enough that the conventions are the real ones, not a guess. Hold what's followed today apart from what's an intended change.

Scale the method to the repo: read directly for a small one; for a large one, dispatch parallel search agents to sample patterns across it, then verify yourself. Test the result against the conventions standards below before drafting.

### 3. Propose

Shape the extracted conventions into a draft, then check it holds.

#### Produce the draft

Fill the template from the analysis: the overview and stack, the project structure, the commands, and the conventions. Add the testing, git, or pitfalls sections only when they carry something the core doesn't. Mark intended changes as intended.

#### Validate

Check that the conventions match the real code — the de-facto patterns, not generic best practice — and that the commands actually run, named from the config rather than guessed. Confirm each rule is one a cold agent could follow.

### 4. Present

Present the draft so the reader can follow it without the code in front of them.

#### The draft

Present the conventions — the best-effort extraction from what you found. It's both the first draft and the thing the user reacts to.

#### Honest account

Close with an honest read: where the conventions are extracted from real patterns, where the code is inconsistent and you picked the dominant one, and what's a proposed change versus current practice.

### 5. Facilitate

Surface the decisions that actually matter — the ones your analysis exposed. Use the draft as something concrete to push against, but draw the questions from the real code.

Be a thinking partner with small batches of questions, considering what the user leans toward before offering your read. Useful angles:

- Where the codebase is inconsistent, and which pattern should be the convention.
- Which rules actually prevent slop, against noise the agent doesn't need.
- What's worth changing versus documenting as-is.

The result can re-affirm the draft, reshape it, or reset which patterns are the conventions. When the conventions reframe, rework the doc as a v2 and present it as such. Before capturing, reflect the settled shape back — the structure, the commands, the key conventions, and anything you'd flag. If the user revises, fold it in and re-confirm rather than writing straight away.

### 6. Capture

Save only when the user asks or confirms. Ask what's next with the blocking-question tool:

- **Refine in conversation (or stop here)** — no file written; the alignment carries forward in conversation.
- **Save** — write the doc per the template and the plugin data location config below, with `last_updated` set to today.

## Conventions standards

The bar a conventions doc clears. A strong doc is:

- **Grounded** — the conventions are extracted from the real code, the patterns it actually follows, not generic best practice.
- **Actionable** — each rule is one a cold agent could follow, concrete rather than aspirational.
- **Operational** — the build, test, and run commands are real and named from the config, not guessed.
- **Lean** — it carries the rules that keep work consistent and prevent slop, not a style encyclopedia.
- **Current and intended kept distinct** — what the code follows today is separated from proposed changes.

## Running autonomously

When asked to run autonomously, skip facilitation.

Instead, run the "Verify on request" step.

## Verify on request

When asked to verify the conventions doc.

Dispatch an adversarial agent to review the draft, briefed to stress-test the conventions; to find where its rules don't hold against the real code by walking through it.
- Don't bias on the results, tell it what to look for, or guess what it'll find.
- Request it to provide only confirmed, valuable findings over minor or unconfirmed ones. No findings are better than wrong ones.

Review and assess the results provided by the agent. Verify each finding it raises. They could be wrong or misled. Incorporate only what is valid and adds value (even if minor enhancements).

## Plugin Data Location Config

Unless specified otherwise, use the plugin data for where to find and save relevant plugin artifacts.
- **Plugin Data Path** — `${user_config.save_path}`, or `.loop-specs` if `save_path` isn't set. Create it if needed.
- **Feature folder** — `<plugin-data-path>/<feature-slug>`.
- **Feature slug** — 2–4 words, hyphenated. Before saving, check the existing folders under the plugin data path for any that clearly match (name and recency). Assume a new slug if none clearly match.
- **Save File Name** — `<feature-folder>/conventions.md`. Fixed, lowercase.

Unsure where it should go? Ask with the blocking-question tool (unless running autonomously). Otherwise assume the defaults and confirm the resolved path in the close.

If the user wants it to live at the repo's `CLAUDE.md` or `AGENTS.md`, or names a path, use that instead.

## Writing style

- Write the doc and everything in chat to prioritize the reader's understanding — plain language, no jargon beyond the domain terms the project genuinely needs.
- Don't narrate the code-reading or your analysis as a frame; use it to shape the conventions.
- Explain what isn't obvious — the agent that follows the doc isn't looking at your analysis.
- Keep questions for the user in their own section — don't bury them in prose.
- Reserve the blocking-question tool for mechanical decisions with clear answers; framing and judgment belong in conversation.


## Argument Flags
If the user arguments includes any of the following flags, follow them as if they are additional instructions:
--save, --autoSave: Once finalized, save the document in the save set without prompting
--autonomous, --auto: Run in autonomous mode. (see: "Running autonomously")
--verify: Run the "Verify on request" step.
