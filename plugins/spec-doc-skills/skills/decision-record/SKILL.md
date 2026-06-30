---
description: Design a decision record (ADR) — one significant decision captured with the context that forced it, the real alternatives, the choice, and the consequences. Use when the user wants to capture why a choice was made so it isn't re-litigated — "record this decision", "write an ADR for X" — rather than map the whole architecture or weigh a still-open product direction.
argument-hint: "[the decision to record — or a de-facto choice in the code to capture]"
---

# Decision Record Designer

Draft and refine a decision record with the user — one significant decision, with the context that forced it, the real alternatives weighed, the choice made, and the consequences. Weigh genuine alternatives, not strawmen, and name what the decision makes harder, not just what it makes easier.

## Process

Read [assets/decision-record-template.md](assets/decision-record-template.md) up front — it's the artifact every step builds toward. Compress a step the work doesn't earn — acknowledge the skip rather than dropping it silently.

### 1. Ground in the decision

Read the codebase and any architecture docs that bear on the decision. Settle what's being decided — and whether it's an open choice or a de-facto one already made in the code — then recap and confirm before recording. 

If it's a routine choice — no real contender, easy to reverse — say so and offer a one-line note instead of a full record. Check the decisions folder for an existing record on this choice; a decision that revisits one supersedes it.

### 2. Analyze

Work out the forces and the real options, and pressure-test them before drafting.

- **Name what forces the decision** — the problem and the constraints that make a choice necessary now.
- **Lay out the genuine alternatives** — each with its real tradeoffs, fairly stated.
- **For a large or contested decision, perform a judgement check.** Dispatch a `spec-doc-skills:judgement-analysis` agent:
  - Ask it to choose and run a Compared-to-what? or Pre-mortem analysis
  - Provide a clean writeup of the problem and constraints

  Don't explain the exercise's steps, tell it what to look for, or guess what it'll find.
- **For a de-facto decision, reconstruct the why from the code** — confirm it matches what the code does, mark reconstructed intent as such, and don't let hindsight make the choice look more inevitable than it was.
- **Test the result against the decision record standards** below before drafting.

### 3. Propose

Shape the analysis into a draft, then check it holds.

#### Produce the draft

Fill the template from the analysis: the context, the options considered with their tradeoffs, the decision and why it wins, and the consequences. Add the related-decisions section only when it carries something the core doesn't.

#### Validate

Check that the options are real alternatives honestly weighed, not strawmen; that the consequences name what gets harder, not only the upside; and — for a de-facto decision — that the recorded choice matches what the code actually does.

### 4. Present

Present the draft so the reader can follow it without the code in front of them.

#### The draft

Present the record — the best-effort capture from what you found. It's both the first draft and the thing the user reacts to.

#### Honest account

Close with an honest read: where the rationale is solid, where it reconstructs intent that wasn't documented, and which consequences are uncertain.

### 5. Facilitate

Surface the decision's real cruxes — the ones your analysis exposed. Use the draft as something concrete to push against, but draw the questions from the forces and the alternatives.

Be a thinking partner with small batches of questions, considering what the user leans toward before offering your read. Useful angles:

- Whether the options are the real ones, or an alternative was dismissed too fast.
- Whether the chosen option still wins once the harder consequences are on the table.
- Whether the context actually forces a decision now, or it could be deferred.

The result can re-affirm the draft, reshape it, or land on a different choice. When the decision changes, rework the record as a v2 and present it as such. Before capturing, reflect the settled shape back — the decision, why it wins, the consequences, and anything you'd flag. If the user revises, fold it in and re-confirm rather than writing straight away.

### 6. Capture

Save only when the user asks or confirms. Ask what's next with the blocking-question tool:

- **Refine in conversation (or stop here)** — no file written; the alignment carries forward in conversation.
- **Save** — write the record per the template and the plugin data location config below. Set `status` to `accepted` if the decision is settled or `proposed` if it's still awaiting one; if this record supersedes an earlier one, mark that one `superseded` and link the two under Related decisions.

## Decision record standards

The bar a decision record clears. A strong record is:

- **Significant** — the decision is worth recording: hard to reverse, constrains future work, or had a genuine close alternative. A routine choice with no real contender is a note, not a record.
- **Real options** — the alternatives are genuine, fairly weighed, not strawmen set up to lose.
- **Honest about consequences** — what the decision makes harder is named alongside what it makes easier.
- **Context-forced** — it shows why a decision is needed, not just what was picked.
- **Specific** — the decision is a concrete choice a reader could act on, not a direction.
- **Grounded** — for a decision already made, the record matches what the code actually does.

## Running autonomously

When asked to run autonomously, skip facilitation.

Instead, run the "Verify on request" step.

## Verify on request

When asked to verify the record.

Dispatch an adversarial agent to review the draft, briefed to stress-test the decision record; to find where its options, rationale, and consequences don't hold by walking through it.
- Don't bias on the results, tell it what to look for, or guess what it'll find.
- Request it to provide only confirmed, valuable findings over minor or unconfirmed ones. No findings are better than wrong ones.

Review and assess the results provided by the agent. Verify each finding it raises. They could be wrong or misled. Incorporate only what is valid and adds value (even if minor enhancements).

## Plugin Data Location Config

Unless specified otherwise, use the plugin data for where to find and save relevant plugin artifacts.
- **Plugin Data Path** — `${user_config.save_path}`, or `.spec-docs/docs` if `save_path` isn't set. Create it if needed.
- **Decisions folder** — `<plugin-data-path>/decisions`.
- **Save File Name** — `<decisions-folder>/NNNN-<short-title>.md`
- **File name** — a four-digit sequence `NNNN` bumped past any existing decision, and a short title.

If the user names a path, use it.

## Writing style

- Write the record and everything in chat to prioritize the reader's understanding — plain language, no jargon beyond the domain terms the decision genuinely needs.
- Don't narrate the code-reading or your analysis as a frame; use it to shape the record.
- Explain what isn't obvious — the reader isn't looking at the code or your analysis.
- Keep questions for the user in their own section — don't bury them in prose.
- Reserve the blocking-question tool for mechanical decisions with clear answers; framing and judgment belong in conversation.
