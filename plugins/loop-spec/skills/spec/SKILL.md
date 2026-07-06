---

## description: Build any spec doc for a product, feature, or autonomous task. Requirements, JTBD, architecture, tech spec, data model, API contract, conventions, glossary, NFRs, threat model, test strategy, QA plan, risk register, assumptions, work breakdown, or task brief. Use when the user wants a task specced ahead of an agent loop or goal, "spec this out", "write the docs for this feature".
argument-hint: "[the task, feature, or system to spec — and any doc types already known to be wanted]"

# Spec Builder

Settle the decisions a task needs settled before execution, and record them in the right docs. A spec's value is the judgment it closes — the choices an executing agent would otherwise resolve by guessing. The docs are the containers; the decisions are the cargo.

Given a task, surface its open decisions, map them to a right-sized collection of specs that holds them, then produce the docs one at a time — running the full per-document process to completion for each before starting the next.

## Steps

1. **Understand the task.** Analyze the task, feature, or system in front of you — enough to see where its real choices lie to align on and predefine to be implemented well.
2. **Consider the open decisions.** Surface the forks: interpretation choices, structural choices, tradeoffs, important risks, details, or core areas for alignment — anything execution would resolve by guessing. Consider if deeper decisions or alignments are needed or would be valuable, as well as the more tactical ones.
3. **Choose the specs needed.** Select a right-sized set from the catalog for the task. Evaluate the spec catalog and choose those that, in aggregate, would provide all the decisions that need to be settled ahead of execution a home. Spec effort scales with the decisions, uncertainty, and chance for misalignment, not the task's size or importance. A doc without unique, meaningful decisions is noise, which will be harmful to execution.
4. **Propose and confirm.** Present the recommended list of specs, in order of dependency and with an explaination on why those were selected and what decisions they help clarify. If available, include a set of 1-3 additional specs which may be worth including in the set that could help clarify other decisions, and an explaination. For the rest, list them as excluded. When unsure whether something makes the set, leave it out and say so.
5. **Produce each doc.** Run the full per-document process below to completion — through capture — for the current doc.
6. **Re-check, then advance.** After each document is complete, before moving on to the next document, you *must* do an evaluation and consider if there are any new specs to add to the plan, or any specs planned that no longer seem valuable. Update the inventory, adjust the remaining set, and raise any change with the user. Repeat until all are complete.

Note: Decisions that are already settled, or best deferred until execution, should be excluded from the spec evaluation.

## Per-document process

For each spec to generate, follow each of the process proceedural steps in order. Read the doc's card (`assets/cards/<doc>.md`) and template (`assets/templates/<doc>.md`) to help guide the work — the card carries this doc's analysis method, the quality bar it must clear, and where its facilitation leverage is; the template is the artifact every step builds toward. Compress a step the work doesn't earn — acknowledge the skip rather than dropping it silently.

### 1. Ground

Ground in what this doc rests on, plus any doc produced earlier in this run, any source doc the user pointed to, and any existing version of this doc. Settle the scope and recap it in a line or two, then confirm before analyzing.

- No existing doc → work the scope in full, then facilitate.
- An existing doc → summarize what's there in a few lines, and work out with the user what to revisit.

### 2. Analyze

Do the doc's real research, grounded in the actual code, config, and docs, not generic knowledge — the work that turns each decision assigned to this doc into a real choice with grounded options. Hold what actually exists apart from what's intended or proposed, and mark the latter as such. When the research surfaces a fork the inventory missed, fold it into the plan.

Scale the method to the surface: read directly for a small or familiar one; for a large or unfamiliar one, dispatch parallel search agents to map it, then verify the load-bearing findings against the source yourself. Test the result against the quality bar before drafting.

### 3. Draft

Fill the template from the analysis. 

- Compress a template section with no decision or finding behind it, and match depth to the work — a small scope gets a lean doc. 
- The doc's substance is its settled decisions. State decisions, not aspirations. 
- Use a diagram or table where it shows the substance better than prose.
- Focus on the unique decisions for this spec. Avoid simply repeating and rephrasing decisions that were already captured in existing specs.

Then validate: check the draft against the quality bar, and verify its load-bearing claims against the source.

### 4. Present

Present the draft so the reader can follow it without the code or your analysis in front of them. It's both the first draft and the thing the user reacts to.

Close with an honest account: where the doc is verified and solid, where it rests on inference or assumption — and what it settles, what it leaves open, and what it defers to execution on purpose.

### 5. Facilitate

Surface the decisions that actually change the doc — the ones your analysis exposed. Use the draft as something concrete to push against, but draw the questions from the real material. 

Where the material exposes a tension between the user's goals, drive it to a settled side.

Be a thinking partner with small batches of questions, considering what the user leans toward before offering your read. The result can re-affirm the draft, reshape it, or reframe it — when the framing changes, rework the doc as a v2 and present it as such. Before capturing, reflect the settled shape back in a few lines; if the user revises, fold it in and re-confirm rather than writing straight away.

### 6. Capture

Save only when the user asks or confirms. Ask what's next with the blocking-question tool:

- **Refine in conversation (or stop here)** — no file written; the alignment carries forward in conversation.
- **Save** — write the doc per the template and the plugin data location config below, with `last_updated` set to today where the template carries it.

When more docs remain in the agreed list, move to the next one after capture.

## Running autonomously

When asked to run autonomously, make the select-and-sequence call yourself — state the list and proceed — and skip facilitation for each doc.

In facilitation's place, run the "Verify on request" step, and save each finished doc.

## Verify on request

When asked to verify a doc.

Dispatch an adversarial agent to review the draft, briefed to stress-test it against what the card says this doc must hold up to — to find where its claims don't hold by walking through them against the real source.

- Don't bias it on the results, tell it what to look for, or guess what it'll find.
- Request only confirmed, valuable findings over minor or unconfirmed ones. No findings are better than wrong ones.

Review and assess the results. Verify each finding it raises — they could be wrong or misled. Incorporate only what is valid and adds value (even if minor enhancements).

## Plugin Data Location Config

Unless specified otherwise, use the plugin data for where to find and save relevant plugin artifacts.

- **Plugin Data Path** — `${user_config.save_path}`, or `.loop-specs` if `save_path` isn't set. Create it if needed.
- **Feature folder** — `<plugin-data-path>/<feature-slug>`. All docs from one run share the feature folder.
- **Feature slug** — 2–4 words, hyphenated. Before saving, check the existing folders under the plugin data path for any that clearly match (name and recency). Assume a new slug if none clearly match.
- **Save File Name** — `<feature-folder>/<doc>.md`, the catalog's output filename for the active doc. Fixed, lowercase.

Unsure where it should go? Ask with the blocking-question tool (unless running autonomously). Otherwise assume the defaults and confirm the resolved path in the close.

## Writing style

- Write the doc and everything in chat to prioritize the reader's understanding — plain language, no jargon beyond the domain terms the work genuinely needs.
- Don't narrate the code-reading or your analysis as a frame; use it to shape the doc.
- Explain what isn't obvious — the reader isn't looking at the code or your analysis.
- Keep questions for the user in their own section — don't bury them in prose.
- Reserve the blocking-question tool for mechanical decisions with clear answers; framing and judgment belong in conversation.

## Argument Flags

If the user arguments include any of the following flags, follow them as if they are additional instructions:
--save, --autoSave: Once finalized, save each document in the save set without prompting
--autonomous, --auto: Run in autonomous mode. (see: "Running autonomously")
--verify: Run the "Verify on request" step on each doc.

## The doc catalog

Each doc type has a spec card at `assets/cards/<doc>.md` and a template at `assets/templates/<doc>.md`, and saves as `<doc>.md`. Load a card only when its doc is about to be produced — never all of them.

Every doc pins down one kind of judgment ahead of execution. The groups run in stage order — earlier groups usually feed later ones.

### Specs Catalog


| Doc                                          | What it's for                                                                                          | Key sections                                                                                                       |
| -------------------------------------------- | ------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------ |
| [requirements](assets/cards/requirements.md) | The what and why of one piece of work — a raw idea explored into options, then settled to a direction. | Problem Statement · Objectives · Who it's for · In / Out of Scope · Requirements · Acceptance Criteria · Key Flows |
| [jtbd](assets/cards/jtbd.md)                 | The durable product frame behind every feature — the job the product is hired for.                     | Main Job · Related Jobs · Emotional & Social Jobs · Success Criteria · User Scenarios                              |
| [nfr](assets/cards/nfr.md)                   | The quality bars the build must clear, as measurable, verifiable targets — not what it does.           | Scope & conditions · Quality targets · Current baseline · Constraints & assumptions                                |


### Design — how the system is shaped


| Doc                                          | What it's for                          | Key sections                                                                                                                                                     |
| -------------------------------------------- | -------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [architecture](assets/cards/architecture.md) | How the system is structured.          | Components · How it fits together · Key decisions · Technology stack · Architectural drivers · Cross-cutting concerns · Runtime & deployment · Risks & tradeoffs |
| [tech-spec](assets/cards/tech-spec.md)       | The design for a piece of work.        | Summary · Goals & non-goals · Proposed design · Alternatives considered · Risks & open questions · Detailed design · Dependencies                                |
| [data-model](assets/cards/data-model.md)     | The shape of the data.                 | Entities · Relationships · Constraints & invariants · Lifecycle & state · Enums & value sets · Storage & indexes                                                 |
| [api-contract](assets/cards/api-contract.md) | The interface consumers build against. | Conventions · Operations · Data types · Invariants & guarantees · Rate limits & quotas · Examples                                                                |


### Patterns — the language and conventions to conform to


| Doc                                        | What it's for                                                                 | Key sections                                                                                                          |
| ------------------------------------------ | ----------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------- |
| [conventions](assets/cards/conventions.md) | The repo-wide rules a cold agent must follow so its work fits.                | Overview & stack · Project structure · Commands · Conventions · Testing conventions · Git & PR conventions · Pitfalls |
| [glossary](assets/cards/glossary.md)       | The domain vocabulary — precise, shared definitions so words stay consistent. | Scope · Terms · Contested terms                                                                                       |


### Plan of work — how the effort is sliced and handed off


| Doc                                              | What it's for                                                           | Key sections                                                                                                     |
| ------------------------------------------------ | ----------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------- |
| [work-breakdown](assets/cards/work-breakdown.md) | The task tree for a large effort, ordered by dependency.                | Tasks · Dependencies & sequence · Sizing · Phases & milestones                                                   |
| [task-brief](assets/cards/task-brief.md)         | One unit of work, packaged so a cold agent can build it without asking. | Task & scope · Context · Starting points · Constraints & conventions · Acceptance & verification · Prerequisites |


### Risk & proof — what could go wrong and how you'll know it's right


| Doc                                            | What it's for                                                                                                    | Key sections                                                                                           |
| ---------------------------------------------- | ---------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------ |
| [assumptions](assets/cards/assumptions.md)     | The beliefs the work rests on, each with a way to validate it. For the exposures they create, use risk-register. | Context · Assumptions (table) · Hypotheses · Validation plan                                           |
| [risk-register](assets/cards/risk-register.md) | What could derail the work, each rated with a response. For the beliefs behind the risks, use assumptions.       | Scope · Risks (table) · Assumptions · Issues · Dependencies                                            |
| [threat-model](assets/cards/threat-model.md)   | The security exposure — what's worth protecting, and how it could be attacked.                                   | Scope & assets · Attack surface · Threats · Mitigations · Trust model & assumptions · Residual risk    |
| [test-strategy](assets/cards/test-strategy.md) | What to test and how deeply, driven by risk. For the runnable pre-ship checklist, use qa-plan.                   | Scope · Risks · Test approach · Scenarios · Coverage & done · Environment & data · Specialized testing |
| [qa-plan](assets/cards/qa-plan.md)             | The concrete pre-ship checks and the exit gate that says it's ready. Usually fed by a test strategy.             | Scope · Checks · Exit criteria · Environments · Regression areas · Entry criteria                      |


