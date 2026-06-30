---
description: Design an assumptions doc — the beliefs a piece of work rests on and the bets it's making, each rated for risk and with a way to validate it, so the riskiest get tested first. Use when the user wants to surface what they're taking for granted — "what are we assuming here", "list the assumptions behind X" — rather than the risks those assumptions create.
argument-hint: "[the work whose assumptions to surface — or a path to its requirements or plan doc]"
---

# Assumptions Designer

Draft and refine an assumptions doc with the user — the beliefs a piece of work takes as true and the bets it's making, each rated for how bad it would be if wrong and how sure we are, with a way to validate it. Surface the load-bearing assumptions, the ones that would sink the work if false, not just the safe and obvious ones.

## Process

Read [assets/assumptions-template.md](assets/assumptions-template.md) up front — it's the artifact every step builds toward. Compress a step the work doesn't earn — acknowledge the skip rather than dropping it silently.

### 1. Ground in the work

Read the requirements or plan doc if one was pointed to, and any existing assumptions doc. Settle the work whose assumptions you're surfacing, then recap before drafting.

### 2. Analyze

Surface the beliefs the work rests on and how risky each is — reaching for the load-bearing ones, the assumptions that would sink the work if wrong, not the safe and obvious.

- **Invert what the plan takes as given.** For each thing it treats as settled, ask what must be true for it to hold. The beliefs that must hold but aren't proven are the load-bearing assumptions — the dangerous ones are those the work reads right past.
- **Separate known from assumed.** What's proven in the code or settled is a fact, not an assumption. Keep the two apart.
- **Rate each assumption** — how critical it is if false, how confident we are, and how it could be validated.

Test the result against the assumptions standards below before drafting.

### 3. Propose

Shape the analysis into a draft, then check it holds.

#### Produce the draft

Fill the template from the analysis: the context, and the assumptions — each with its criticality, confidence, and how to validate it — ranked riskiest first. Add the hypotheses or validation-plan sections when the work has explicit bets to test. The risk ratings are proposals for the user to confirm.

#### Validate

Check that each item is genuinely an assumption, not an established fact; that the load-bearing ones are surfaced, not just the comfortable ones; and that the riskiest — critical and uncertain — lead.

### 4. Present

Present the draft so the reader can follow it without the code in front of them.

#### The draft

Present the assumptions — the best-effort surfacing from what you found. It's both the first draft and the thing the user reacts to.

#### Honest account

Close with an honest read: where an assumption is grounded enough to be near-fact, which are the real leap-of-faith bets, and which ratings you're least sure of. Flag any high-confidence rating that rests on hope rather than evidence — those are the ones to confirm with the user before locking them in.

### 5. Facilitate

Surface the decisions that actually matter — the ones your analysis exposed. Use the draft as something concrete to push against, but draw the questions from what the work really rests on.

Be a thinking partner with small batches of questions, considering what the user leans toward before offering your read. Useful angles:

- Which assumption, if wrong, would hurt the most — and whether it's been tested.
- Whether something listed as an assumption is actually known, or the reverse.
- Which leap-of-faith bets are worth validating before building.

The result can re-affirm the draft, reshape it, or surface a bigger assumption hiding under the others. When that happens, rework the register and re-present what changed. Before capturing, reflect the settled shape back — the riskiest assumptions, their validation, and anything you'd flag. If the user revises, fold it in and re-confirm rather than writing straight away.

### 6. Capture

Save only when the user asks or confirms. Ask what's next with the blocking-question tool:

- **Refine in conversation (or stop here)** — no file written; the alignment carries forward in conversation.
- **Save** — write the doc per the template and the plugin data location config below, with `last_updated` set to today.

## Assumptions standards

The bar an assumptions doc clears. A strong doc is:

- **Genuinely assumptions** — each is a belief taken as true, not an established fact dressed up as one.
- **Load-bearing surfaced** — the risky, unstated assumptions are named, not just the safe obvious ones.
- **Rated** — each carries how critical it is if wrong and how confident we are, so the register can be ranked.
- **Testable** — each has a way it could be validated, even if that's "run a spike."
- **Ranked** — the critical-and-uncertain assumptions lead; the safe ones don't bury them.

## Running autonomously

When asked to run autonomously, skip facilitation.

Instead, run the "Verify on request" step.

## Verify on request

When asked to verify the doc.

Dispatch a `spec-doc-skills:judgement-analysis` agent to stress-test the draft:

* Ask it to run the Pre-mortem exercise
* Provide a clean writeup of the work

Don't explain the exercise's steps, tell it what to look for, or guess what it'll find. Request only confirmed, valuable findings over minor or unconfirmed ones — no findings are better than wrong ones.

Review and assess the results provided by the agent. Verify each finding it raises. They could be wrong or misled. Incorporate only what is valid and adds value (even if minor enhancements).

## Plugin Data Location Config

Unless specified otherwise, use the plugin data for where to find and save relevant plugin artifacts.
- **Plugin Data Path** — `${user_config.save_path}`, or `.spec-docs/docs` if `save_path` isn't set. Create it if needed.
- **Assumptions folder** — `<plugin-data-path>/assumptions`.
- **Save File Name** — `<assumptions-folder>/<topic>-assumptions.md`.
- **File name** — the topic; update it in place when revisiting.

If the user names a path, use it.

## Writing style

- Write the doc and everything in chat to prioritize the reader's understanding — plain language, no jargon beyond the domain terms the work genuinely needs.
- Don't narrate the analysis as a frame; use it to shape the assumptions.
- Explain what isn't obvious — the reader isn't looking at the code or your analysis.
- Keep questions for the user in their own section — don't bury them in prose.
- Reserve the blocking-question tool for mechanical decisions with clear answers; framing and judgment belong in conversation.
