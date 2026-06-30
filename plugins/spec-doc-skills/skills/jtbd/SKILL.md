---
description: Design or refine a JTBD doc — the main job a product is hired for, the criteria users judge it by, and the scenarios it should serve. Use when the user wants to define or revisit the jobs and user scenarios behind a product — "write our JTBD", "map the user scenarios" — naming the job the product serves rather than the solution that serves it.
argument-hint: "[the product to define the jobs and scenarios for — defaults to the current product]"
---

# JTBD Designer

Draft and refine a JTBD doc with the user — the main job the product is hired for, the success criteria, and the user scenarios that show it in action. It grounds directly in what the product is *for*: the job and the situations the product serves. It stays at the level of the job — no problem statement, no metrics, and no solution or feature spec.

The doc helps the user decide what to build next, so the scenarios are its core — each concrete enough to build toward and to check a build against. The main job and criteria stay durable across feature changes; the scenarios stay sharp and build-pointing.

## Process

Thoughtfully design, write, and refine the JTBD doc in session with the user — facilitating to get the best result, saving only when requested or confirmed. Compress a step the work doesn't earn — acknowledge the skip rather than dropping it silently.

### 1. Ground in the product's purpose

Read any existing JTBD doc, then ground on what the product is *for* — the README, the app, and the code where it sharpens the picture, plus what the user tells you about the product and its users. The JTBD and user scenarios this doc defines describe the target state, not the current one.

- No JTBD doc → draft the full doc, then facilitate.
- An existing JTBD doc → summarize what's there in a few lines, and work out with the user what to revisit.

When there's little to ground in and the user gives no direction, say so and work from what the user tells you about the product and its users; the job and scenarios still ground in something real.

### 2. Analyze

From the product's purpose, work out what the product is really hired for: the main job, the success criteria users judge it by, and the 5–8 situations where the job shows up. This is the reasoning move — what the job *is* — before it's committed to the draft.

### 3. Propose

Shape the worked-out job into a draft, then check it holds.

#### Produce the draft

Produce the main job, the success criteria, and the user scenarios, using [assets/jtbd-template.md](assets/jtbd-template.md) as the target and requirements. 

#### Validate

Check the draft holds against the product's real purpose. Each scenario should be concrete enough to build toward and to check a build against. Resolve the gaps before presenting.

### 4. Present

Present the draft so the reader can follow it without the app or your analysis in front of them.

#### The draft

Present the JTBD and user scenarios. This is the best-effort representation based on the information you have — thoughtfully decided and presented. It serves as both the first draft and what the user reacts to.

#### Honest account

Close with a short, plain explanation of what the proposal reflects — the job the product is hired for and the situations it serves — and an honest read of it: where the job and scenarios are solid, where they rest on assumptions about intent, and what's known versus still unknown.

### 5. Facilitate

Consider what's genuinely unsettled about the job and its scenarios, based on your analysis so far. Help the user see the framing decisions that matter — the inflection points, the implications, and what they actually want.

- Use the draft as a facilitation mechanism — a concrete thing to push against — but the depth is in the product's purpose.
- Draw your questions from that depth: the assumptions the draft rests on, and the real questions underneath that would shift the job or the scenarios.

Facilitate by asking thoughtful questions to uncover insights like:

- Whether the job is framed at the right altitude and scope at all.
- Whether it fits the user's real intent better or worse than the draft assumes.
- Whether the conversation points to a stronger framing of the job — or a more telling set of scenarios — than the draft captured.

Be a thinking partner with small batches of questions at a time, considering what they lean toward before offering your own read. With a concrete draft in front of them, putting a few alternatives out to react to is fair — in conversation.

The result can re-affirm the current draft, reshape it, or reach something new the conversation found. If a fundamental reclarification, new core insight, or reframing would redefine the job or ripple more widely, rethink the draft as a v2 and present it as such based on the learnings.

Before capturing, reflect the settled shape back: the main job, the situations that anchor it, and anything you'd flag. Keep it short. If the user revises, fold it in and re-confirm rather than writing straight away.

### 6. Capture

Save only when the user asks or confirms. When they do, write the doc per the template and the plugin data location config below, with `last_updated` set to today.

## Running autonomously

When asked to run autonomously, skip facilitation.

Instead, run the "Verify on request" step.

## Verify on request

When asked to verify the doc.

Dispatch an adversarial agent to review the draft, briefed to stress-test the JTBD; to find where its main job, success criteria, and scenarios don't hold by walking through it.
- Don't bias on the results, tell it what to look for, or guess what it'll find.
- Request it to provide only confirmed, valuable findings over minor or unconfirmed ones. No findings are better than wrong ones.

Review and assess the results provided by the agent. Verify each finding it raises. They could be wrong or misled. Incorporate only what is valid and adds value (even if minor enhancements).

## Plugin Data Location Config

Unless specified otherwise, use the plugin data for where to find and save relevant plugin artifacts.
- **Plugin Data Path** — `${user_config.save_path}`, or `.spec-docs/docs` if `save_path` isn't set. Create it if needed.
- **JTBD folder** — `<plugin-data-path>/jtbd`.
- **Save File Name** — `<jtbd-folder>/JTBD.md`.
- **File name** — always `JTBD.md`.

If the user names a path, use it.

## Writing style

- Whether it's the doc and in chat, write to prioritize the reader's understanding — plain language, no jargon. Domain-specific language is often valuable and necessary for clear communication; that is reasonable and ok.
- Don't narrate the grounding or your analysis as a frame; use it to shape the doc.
- Explain what isn't obvious — the reader isn't looking at the app or your analysis.
- Keep questions for the user in their own sections, not buried in prose.
- Reserve the blocking-question tool for mechanical decisions with clear answers; framing and judgment belong in conversation.
