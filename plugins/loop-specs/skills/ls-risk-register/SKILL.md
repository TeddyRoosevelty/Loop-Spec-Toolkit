---
description: Design a risk register — the risks facing a body of work, each with its likelihood, impact, and response, expanding to the full RAID (assumptions, issues, dependencies) when warranted. Use when the user wants to surface and track what could derail something — "what are the risks", "build a risk register for X" — rather than run a one-off premortem exercise.
argument-hint: "[the work or system to assess — or a path to its plan or requirements doc]"
---

# Risk Register Designer

Draft and refine a risk register with the user — the risks facing a body of work, each with its likelihood, impact, and a response, expanding to assumptions, issues, and dependencies when the work warrants the full RAID. Surface this work's real risks, not generic boilerplate, and give each one a response.

## Process

Read [assets/risk-register-template.md](assets/risk-register-template.md) up front — it's the artifact every step builds toward. Compress a step the work doesn't earn — acknowledge the skip rather than dropping it silently.

### 1. Ground in the work

Read the plan or requirements doc if one was pointed to, and any existing register. Settle what the register covers — the work, system, or timeframe — and recap it before assessing.

- No register → assess the scope in full, then facilitate.
- An existing register → summarize what's there, update the statuses, and work out with the user what to revisit.

### 2. Analyze

Surface what could derail the work and how to respond.

- **Find risks across the angles.** Technical (from the code — fragile areas, dependencies, integrations), product and delivery (from the user jobs and scope), and the assumptions the work rests on.
- **Rate and respond.** For each real risk, assess its likelihood and impact and decide a response.

For a substantial body of work, dispatch a `loop-specs:judgement-analysis` agent:

* Ask it to run the Pre-mortem exercise
* Provide a clean writeup of the work

Don't explain the exercise's steps, tell it what to look for, or guess what it'll find. Then organize what it surfaces into the register. 

For a small body of work, work it in session instead. Test the result against the risk standards below before drafting.

### 3. Propose

Shape the analysis into a draft, then check it holds.

#### Produce the draft

Fill the template from the analysis: the scope, and the risk register — each risk with its likelihood, impact, and response, ranked by severity. Add the assumptions, issues, or dependencies sections when the work warrants the full RAID.

#### Validate

Check that each risk is specific to this work and traceable to something real, not boilerplate; that each has a response; and that the register is ranked so the severe risks lead.

### 4. Present

Present the draft so the reader can follow it without the code in front of them.

#### The draft

Present the register — the best-effort assessment from what you found. It's both the first draft and the thing the user reacts to.

#### Honest account

Close with an honest read: where the risks are grounded and assessed, which rest on assumptions, and the uncomfortable ones worth not glossing over.

### 5. Facilitate

Surface the risk decisions that actually matter — the ones your analysis exposed. Use the draft as something concrete to push against, but draw the questions from the code, the user jobs, and the scope.

Be a thinking partner with small batches of questions, considering what the user leans toward before offering your read. Useful angles:

- Whether the severe risks are the real ones, or something bigger is unnamed.
- Whether each response is enough, or just acknowledges the risk.
- Which assumptions, if wrong, would hurt the most.

The result can re-affirm the draft, reshape it, or reorder the register. When a bigger risk surfaces, rework it as a v2 and present it as such. Before capturing, reflect the settled shape back — the severe risks, their responses, and anything you'd flag. If the user revises, fold it in and re-confirm rather than writing straight away.

### 6. Capture

Save only when the user asks or confirms. Ask what's next with the blocking-question tool:

- **Refine in conversation (or stop here)** — no file written; the alignment carries forward in conversation.
- **Save** — write the register per the template and the plugin data location config below, with `last_updated` set to today.

## Risk standards

The bar a risk register clears. A strong register is:

- **Specific** — each risk is this work's real exposure, traceable to the code, user jobs, or scope, not generic boilerplate.
- **Assessed** — each carries a likelihood and an impact, so the register can be ranked.
- **Actionable** — each has a response: mitigate, accept, avoid, or transfer — not just a statement of dread.
- **Ranked** — it leads with the severe risks (likelihood × impact), not the order they were found.
- **Honest** — the uncomfortable risks are named, not smoothed over.

## Running autonomously

When asked to run autonomously, skip facilitation.

Instead, run the "Verify on request" step.

## Verify on request

When asked to verify the register.

Dispatch an adversarial agent to review the draft, briefed to stress-test the register; to find where its risks, ratings, and responses don't hold by walking through it.
- Don't bias on the results, tell it what to look for, or guess what it'll find.
- Request it to provide only confirmed, valuable findings over minor or unconfirmed ones. No findings are better than wrong ones.

Review and assess the results provided by the agent. Verify each finding it raises. They could be wrong or misled. Incorporate only what is valid and adds value (even if minor enhancements).

## Plugin Data Location Config

Unless specified otherwise, use the plugin data for where to find and save relevant plugin artifacts.
- **Plugin Data Path** — `${user_config.save_path}`, or `.loop-specs` if `save_path` isn't set. Create it if needed.
- **Feature folder** — `<plugin-data-path>/<feature-slug>`.
- **Feature slug** — 2–4 words, hyphenated. Before saving, check the existing folders under the plugin data path for any that clearly match (name and recency). Assume a new slug if none clearly match.
- **Save File Name** — `<feature-folder>/risk-register.md`. Fixed, lowercase.

Unsure where it should go? Ask with the blocking-question tool (unless running autonomously). Otherwise assume the defaults and confirm the resolved path in the close.

## Writing style

- Write the register and everything in chat to prioritize the reader's understanding — plain language, no jargon beyond the domain terms the work genuinely needs.
- Don't narrate the analysis as a frame; use it to shape the register.
- Explain what isn't obvious — the reader isn't looking at the code or your analysis.
- Keep questions for the user in their own section — don't bury them in prose.
- Reserve the blocking-question tool for mechanical decisions with clear answers; framing and judgment belong in conversation.


## Argument Flags
If the user arguments includes any of the following flags, follow them as if they are additional instructions:
--save, --autoSave: Once finalized, save the document in the save set without prompting
--autonomous, --auto: Run in autonomous mode. (see: "Running autonomously")
--verify: Run the "Verify on request" step.
