---
description: Design a test strategy — a risk-driven plan for proving a body of work correct: what to test, at which levels, and how much coverage is enough, grounded in the real test setup. Use when the user wants to decide how to prove something works — "how should we test this", "write a test strategy for X" — rather than the pre-ship checklist that verifies a change is ready (the QA plan).
argument-hint: "[the feature, change, or system to test — or a path to its plan or requirements doc]"
---

# Test Strategy Designer

Draft and refine a test strategy with the user — how the correctness of a body of work gets proven: the risks worth testing for, the test levels and what each must establish, the scenarios to cover, and the bar that says it's tested enough. Drive coverage by risk, and prove behavior rather than that code ran.

## Process

Read [assets/test-strategy-template.md](assets/test-strategy-template.md) up front — it's the artifact every step builds toward. Compress a step the work doesn't earn — acknowledge the skip rather than dropping it silently.

### 1. Ground in the work

Read the plan or requirements doc if one was pointed to, and carry its behavior, scope, and acceptance criteria forward. Read the codebase's existing test setup — framework, conventions, CI, and what's already covered. Recap what's being tested and confirm the scope before planning.

### 2. Analyze

Work out what could go wrong and how to catch it.

- **Rank the risks by likelihood × impact.** Depth follows the ranking — areas high on both earn the deepest testing; areas low on both get a line. Likely-to-break signals: complexity, new or unfamiliar code, churn, thin existing coverage, anything stateful or concurrent. Costly-if-broken signals: money, auth and permissions, data integrity, irreversible actions, a wide user-facing blast radius.
- **For each risk, pick the level and the cases.** Cover the dimensions that apply — happy path, edge cases, error paths, integration. Choose the level by what a cheaper one can't prove: a higher level (integration, end-to-end) earns its cost only where a unit test can't pin the behavior down, like a contract across components or state that mocks would assume away.
- **If the work isn't testable as written, say what has to change first.** Untested legacy, no seam, hidden dependencies — name the seam or characterization test needed, rather than planning tests that can't be written.
- **Scale the method to the surface.** Read directly for a small change; for a large one, dispatch parallel search agents to map the existing coverage and test setup, then verify yourself.
- **Ground it and check it before drafting.** Use the repo's real test tooling, and test the result against the test strategy standards below.

### 3. Propose

Shape the analysis into a draft, then check it holds.

#### Produce the draft

Fill the template from the analysis: the scope, the risks, the test approach by level, the scenarios by dimension, and the coverage-and-done bar. Match depth to risk — a config change gets a line, a payment flow a layered approach. Add a conditional section only when it carries something the core doesn't.

#### Validate

Check the two things easiest to miss: no high-risk area is left with shallow or no coverage, and the approach uses the repo's real test tooling — no framework or level the project doesn't have or hasn't committed to adopting. Confirm the scenarios name what to verify, not the test code.

#### Pressure-test the framing (high-risk work)

On high-risk work — auth, payments, data integrity — dispatch an adversarial agent with the behavior under test and the draft, briefed to find the production incident this plan would not catch. 
- Don't bias on the results, tell it what to look for, or guess what it'll find. 
- Request it to provide only confirmed, high value scenarios over minor or unconfirmed ones. No scenarios are better than wrong ones.

Verify each scenario it raises. They could be wrong or misled. Incorporate only what would add value. 

### 4. Present

Present the draft so the reader can follow it without the code in front of them.

#### The draft

Present the plan — the best-effort strategy from what you found. It's both the first draft and the thing the user reacts to.

#### Honest account

Close with an honest read: where coverage is solid, which risks are deliberately left uncovered and why, and what rests on assumptions about how the code behaves.

### 5. Facilitate

Surface the testing decisions that actually matter — the ones your analysis exposed. Use the draft as something concrete to push against, but draw the questions from the risks and the code.

Be a thinking partner with small batches of questions, considering what the user leans toward before offering your read. Useful angles:

- Whether the riskiest areas are getting the deepest testing.
- Where a level — integration, end-to-end — would prove something unit tests can't.
- Which gaps are acceptable to leave uncovered, against the cost of covering them.

The result can re-affirm the draft, reshape it, or restructure the plan. When the risk picture reframes, rework it as a v2 and present it as such. Before capturing, reflect the settled shape back — the risks, the approach, the coverage bar, and anything you'd flag. If the user revises, fold it in and re-confirm rather than writing straight away.

### 6. Capture

Save only when the user asks or confirms. Ask what's next with the blocking-question tool:

- **Refine in conversation (or stop here)** — no file written; the alignment carries forward in conversation.
- **Save** — write the plan per the template and the plugin data location config below.

## Test strategy standards

The bar a test strategy clears. A strong strategy is:

- **Risk-driven** — depth follows risk; the areas most likely to break or most costly get the most coverage, and trivial areas get a line.
- **Behavior-proving** — tests establish what the code does, not that lines executed; coverage numbers are not the goal.
- **At the right altitude** — it names the cases to verify and the level for each, not the test code itself.
- **Honest about gaps** — what's left uncovered is named and justified, not silently omitted.
- **Grounded in the real setup** — the levels and tooling are ones the project actually has or will adopt, not generic.

## Running autonomously

When asked to run autonomously, skip facilitation.

Instead, run the "Verify on request" step.

## Verify on request

When asked to verify the plan.

Dispatch an adversarial agent to review the draft, briefed to stress-test the test strategy; to find where its risk ranking and coverage don't hold by walking through it.
- Don't bias on the results, tell it what to look for, or guess what it'll find.
- Request it to provide only confirmed, valuable scenarios over minor or unconfirmed ones. No scenarios are better than wrong ones.

Review and assess the results provided by the agent. Verify each scenario it raises. They could be wrong or misled. Incorporate only what is valid and adds value (even if minor enhancements).

## Plugin Data Location Config

Unless specified otherwise, use the plugin data for where to find and save relevant plugin artifacts.
- **Plugin Data Path** — `${user_config.save_path}`, or `.loop-specs` if `save_path` isn't set. Create it if needed.
- **Feature folder** — `<plugin-data-path>/<feature-slug>`.
- **Feature slug** — 2–4 words, hyphenated. Before saving, check the existing folders under the plugin data path for any that clearly match (name and recency). Assume a new slug if none clearly match.
- **Save File Name** — `<feature-folder>/test-strategy.md`. Fixed, lowercase.

Unsure where it should go? Ask with the blocking-question tool (unless running autonomously). Otherwise assume the defaults and confirm the resolved path in the close.

## Writing style

- Write the plan and everything in chat to prioritize the reader's understanding — plain language, no jargon beyond the domain terms the work genuinely needs.
- Don't narrate the context-gathering or your analysis as a frame; use it to shape the plan.
- Explain what isn't obvious — the reader isn't looking at the code or your analysis.
- Keep questions for the user in their own section — don't bury them in prose.
- Reserve the blocking-question tool for mechanical decisions with clear answers; framing and judgment belong in conversation.
