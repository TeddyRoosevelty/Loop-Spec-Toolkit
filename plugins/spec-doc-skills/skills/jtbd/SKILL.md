---
description: Design or refine a JTBD doc — the main job a product is hired for, the criteria users judge it by, and the scenarios it should serve. Use when the user wants to define or revisit the jobs and user scenarios behind a product — "write our JTBD", "map the user scenarios" — building on the strategy rather than setting it.
argument-hint: "[optional: section to revisit, e.g. 'scenarios' or 'main job']"
---

# JTBD Designer

Draft and refine a JTBD doc with the user — the main job the product is hired for, the success criteria, and the user scenarios that show it in action. It builds on `STRATEGY.md`: the strategy sets the problem and approach; this doc names the job and the situations the product serves. A companion to the strategy, not a strategy — no problem statement, metrics, or tracks.

The doc helps the user decide what to build next, so the scenarios are its core — each concrete enough to build toward and to check a build against. The main job and criteria stay durable across feature changes; the scenarios stay sharp and build-pointing.

## Process

Thoughtfully design, write, and refine the JTBD doc in session with the user — facilitating to get the best result, saving only when requested or confirmed. Compress a step the work doesn't earn — acknowledge the skip rather than dropping it silently.

### 1. Ground on the strategy and purpose

Read `STRATEGY.md` and any existing JTBD doc. Do light grounding on what the product is *for* — from the strategy first, and a light read of the README or app only where it sharpens that. The JTBD and user scenarios this doc defines describe the target state, not the current one.

This task could be adding or revisiting the JTBD doc:

- No JTBD doc → draft the full doc, then facilitate.
- A JTBD doc → summarize what's there in a few lines, work with the user to understand what should be revisited.
- Provided a section for revisiting → revisit just that section, leave the rest.
- A change on core strategy or a new direction → consider the doc as a whole and the structural changes that reflect throughout.

When there's no `STRATEGY.md` or no anchoring strategy provided, say so — this doc builds on it. Offer to work from what the user tells you about the product, or to set the strategy first with the skill `strategy`.

### 2. Analyze

From the strategy and the product's purpose, work out what the product is really hired for: the main job, the success criteria users judge it by, and the 5–8 situations where the job shows up. This is the reasoning move — what the job *is* — before it's committed to the draft.

### 3. Propose

Shape the worked-out job into a draft, then check it holds.

#### Produce the draft

Produce the main job, the success criteria, and the user scenarios, using [assets/jtbd-template.md](assets/jtbd-template.md) as the target and requirements. 

#### Validate

Check the draft holds against the strategy and the product's real purpose. Each scenario should be concrete enough to build toward and to check a build against. Resolve the gaps before presenting.

### 4. Present

Present the draft so the reader can follow it without the strategy, the app, or your analysis in front of them.

#### The draft

Present the JTBD and user scenarios. This is the best-effort representation based on the information you have — thoughtfully decided and presented. It serves as both the first draft and what the user reacts to.

#### Honest account

Close with a short, plain explanation of what the proposal reflects — the job the product is hired for and the situations it serves — and an honest read of it: where the job and scenarios are solid, where they rest on assumptions about intent, and what's known versus still unknown.

### 5. Facilitate

Consider what's genuinely unsettled about the job and its scenarios, based on the strategy and your analysis so far. Help the user see the framing decisions that matter — the inflection points, the implications, and what they actually want.

- Use the draft as a facilitation mechanism — a concrete thing to push against — but the depth is in the strategy and the product's purpose.
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

If something learned would reshape an existing strategy doc, offer a refinement to it — **only** when it meets the high bar of being strategic direction, or is a reasonably-sized misalignment with the strategy provided.

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
- **Save File Name** — `<plugin-data-path>/JTBD.md`, beside `STRATEGY.md`.
- **File name** — always `JTBD.md`.

If the user names a path, use it.

## Writing style

- Whether it's the doc and in chat, write to prioritize the reader's understanding — plain language, no jargon. Domain-specific language is often valuable and necessary for clear communication; that is reasonable and ok.
- Don't narrate the strategy-reading or your analysis as a frame; use it to shape the doc.
- Explain what isn't obvious — the reader isn't looking at the strategy, the app, or your analysis.
- Keep questions for the user in their own sections, not buried in prose.
- Reserve the blocking-question tool for mechanical decisions with clear answers; framing and judgment belong in conversation.
