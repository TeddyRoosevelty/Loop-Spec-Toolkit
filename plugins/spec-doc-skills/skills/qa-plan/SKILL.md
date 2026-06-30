---
description: Design a QA plan — the concrete checks to run before shipping a change: automated, manual, and exploratory, with the exit gate that says it's ready, grounded in the real test setup. Use when the user wants a runnable pre-release verification checklist — "what should we check before shipping X", "write the QA plan" — rather than the test strategy that decides what to test.
argument-hint: "[the change or release to verify — or a path to its plan or test strategy]"
---

# QA Plan Designer

Draft and refine a QA plan with the user — the concrete checks to run before shipping a change: the automated, manual, and exploratory verification, and the exit gate that says it's ready. Make each check runnable with a clear pass condition, and set an objective gate for shipping.

## Process

Read [assets/qa-plan-template.md](assets/qa-plan-template.md) up front — it's the artifact every step builds toward. Compress a step the work doesn't earn — acknowledge the skip rather than dropping it silently.

### 1. Ground in the change

Read the plan or test strategy if one was pointed to, and the codebase's test setup — suites, tools, CI. Settle what's being verified and how risky it is, then recap before planning.

### 2. Analyze

Work out what to check before shipping and how. From the change and its risks, decide the checks — which automated suites to run, what to check manually, where to explore, what smoke tests to run after deploy. For each, settle how it's run and what passing looks like, and the existing behavior worth re-checking. Test the result against the verification standards below before drafting.

### 3. Propose

Shape the analysis into a draft, then check it holds.

#### Produce the draft

Fill the template from the analysis: the scope, the checks with how-to-run and pass conditions, and the exit criteria. Add the environments, regression, or entry-criteria sections when the change needs them.

#### Validate

Check that each check is concrete and runnable with a clear pass condition, the exit gate is objective, and the regression areas for this change are covered. Confirm the checks use the project's real suites and tools.

### 4. Present

Present the draft so the reader can follow it without the code in front of them.

#### The draft

Present the plan — the best-effort verification from what you found. It's both the first draft and the thing the user reacts to.

#### Honest account

Close with an honest read: where the checks are concrete and grounded, what's left unverified and why, and the riskiest area the plan leans on manual checking for.

### 5. Facilitate

Surface the decisions that actually matter — the ones your analysis exposed. Use the draft as something concrete to push against, but draw the questions from the change's risks.

Be a thinking partner with small batches of questions, considering what the user leans toward before offering your read. Useful angles:

- Whether the checks actually cover the change's risks.
- What existing behavior could regress and isn't being re-checked.
- Whether the exit gate is objective enough to make a clean go/no-go.

The result can re-affirm the draft, reshape it, or tighten the gate. When the verification reframes, rework the plan as a v2 and present it as such. Before capturing, reflect the settled shape back — the checks, the exit gate, and anything you'd flag. If the user revises, fold it in and re-confirm rather than writing straight away.

### 6. Capture

Save only when the user asks or confirms. Ask what's next with the blocking-question tool:

- **Refine in conversation (or stop here)** — no file written; the alignment carries forward in conversation.
- **Save** — write the plan per the template and the plugin data location config below.

## Verification standards

The bar a QA plan clears. A strong plan is:

- **Runnable** — each check is concrete, with how to run it and what passing looks like, not "test the feature."
- **Gated** — the exit criteria are objective, so the ship decision is a clean go/no-go.
- **Regression-aware** — the existing behavior the change could break is named and re-checked.
- **Grounded** — the checks use the project's real suites, tools, and environments.
- **Honest** — what's left unverified is named, not implied away.

## Running autonomously

When asked to run autonomously, skip facilitation.

Instead, run the "Verify on request" step.

## Verify on request

When asked to verify the plan.

Dispatch an adversarial agent to review the draft, briefed to stress-test the QA plan; to find where its checks and exit gate don't hold by walking through it.
- Don't bias on the results, tell it what to look for, or guess what it'll find.
- Request it to provide only confirmed, valuable findings over minor or unconfirmed ones. No findings are better than wrong ones.

Review and assess the results provided by the agent. Verify each finding it raises. They could be wrong or misled. Incorporate only what is valid and adds value (even if minor enhancements).

## Plugin Data Location Config

Unless specified otherwise, use the plugin data for where to find and save relevant plugin artifacts.
- **Plugin Data Path** — `${user_config.save_path}`, or `.spec-docs` if `save_path` isn't set. Create it if needed.
- **Feature folder** — `<plugin-data-path>/<feature-slug>`.
- **Feature slug** — 2–4 words, hyphenated. Before saving, check the existing folders under the plugin data path for any that clearly match (name and recency). Assume a new slug if none clearly match.
- **Save File Name** — `<feature-folder>/qa-plan.md`. Fixed, lowercase.

Unsure where it should go? Ask with the blocking-question tool (unless running autonomously). Otherwise assume the defaults and confirm the resolved path in the close.

## Writing style

- Write the plan and everything in chat to prioritize the reader's understanding — plain language, no jargon beyond the domain terms the work genuinely needs.
- Don't narrate the context-gathering or your analysis as a frame; use it to shape the plan.
- Explain what isn't obvious — the reader isn't looking at the code or your analysis.
- Keep questions for the user in their own section — don't bury them in prose.
- Reserve the blocking-question tool for mechanical decisions with clear answers; framing and judgment belong in conversation.
