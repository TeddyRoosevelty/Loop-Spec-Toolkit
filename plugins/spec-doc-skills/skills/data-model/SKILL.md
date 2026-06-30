---
description: Design a data model doc — the entities a system holds, their fields and types, the relationships between them, and the rules that govern the data, grounded in the real schema. Use when the user wants to capture or design the shape of a system's data — "document the data model", "design the schema for X" — rather than the interface that exposes it or the component structure around it.
argument-hint: "[the system, domain, or feature to model]"
---

# Data Model Designer

Draft and refine a data model with the user — the entities a system holds, their fields and types, the relationships between them, and the rules that govern the data. Describe the real schema where one exists, and mark proposed entities as proposed.

## Process

Read [assets/data-model-template.md](assets/data-model-template.md) up front — it's the artifact every step builds toward. Compress a step the work doesn't earn — acknowledge the skip rather than dropping it silently.

### 1. Ground in the data

Read any existing data model doc. Settle the scope — the whole system, one domain, or a feature — and recap what data is in play, then confirm before modeling.

- No doc → model the scope in full, then facilitate.
- An existing doc → summarize what's there in a few lines, and work out with the user what to revisit.

### 2. Analyze

Read the real data shape from the code: the entities, their fields and types, keys, relationships, and the constraints — from models, schema, and migrations. Hold what the schema actually defines apart from what's only proposed.

Scale the method to the schema: read directly for a small one; for a large one, dispatch parallel search agents to map the entities and relationships, then verify against the source yourself. Test the result against the data model standards below before drafting.

### 3. Propose

Shape the read schema into a draft, then check it holds.

#### Produce the draft

Fill the template from the analysis: the overview, the entities with their fields and keys, the relationships with cardinality, and the constraints and invariants. Use an ERD where it shows the structure better than prose. Add a conditional section only when it carries something the core doesn't, and match depth to the model.

#### Validate

Verify entities, fields, types, and relationships against the source — they match the real schema, with nothing invented or missed. For a new model, confirm it's internally consistent: every relationship references a defined entity, and every entity has a key. Confirm proposed entities read as proposed.

### 4. Present

Present the draft so the reader can follow it without the code in front of them.

#### The draft

Present the model — the best-effort map from what you found. It's both the first draft and the thing the user reacts to.

#### Honest account

Close with an honest read: where the model is verified against the schema, where it rests on inference, and what's existing versus proposed.

### 5. Facilitate

Surface the modeling decisions that actually matter — the ones your analysis exposed. Use the draft as something concrete to push against, but draw the questions from the schema and how the data is really used.

Be a thinking partner with small batches of questions, considering what the user leans toward before offering your read. Useful angles:

- Whether the entities are split where they should be, or a concept is wrongly split or merged.
- Whether the relationships and cardinality match how the data is really used.
- Which invariants must always hold, and whether the model enforces them.

The result can re-affirm the draft, reshape it, or restructure the model. When the structure reframes, rework it as a v2 and present it as such. Before capturing, reflect the settled shape back — the entities, their relationships, the key invariants, and anything you'd flag. If the user revises, fold it in and re-confirm rather than writing straight away.

### 6. Capture

Save only when the user asks or confirms. Ask what's next with the blocking-question tool:

- **Refine in conversation (or stop here)** — no file written; the alignment carries forward in conversation.
- **Save** — write the doc per the template and the plugin data location config below, with `last_updated` set to today.

## Data model standards

The bar a data model clears. A strong model is:

- **Accurate to the schema** — entities, fields, types, and relationships match what's actually defined, verified rather than assumed.
- **Complete** — each entity has a key and typed fields; no entity is a bag of untyped attributes.
- **Relationships explicit** — cardinality and the linking keys are stated, not implied.
- **Constraints captured** — uniqueness, validation, referential integrity, and invariants that must always hold are named.
- **At the right altitude** — a logical model of entities and relationships, not migration SQL or ORM boilerplate.

## Running autonomously

When asked to run autonomously, skip facilitation.

Instead, run the "Verify on request" step.

## Verify on request

When asked to verify the data model.

Dispatch an adversarial agent to review the draft, briefed to stress-test the model; to find where its entities, relationships, and constraints don't hold against the schema by walking through it.
- Don't bias on the results, tell it what to look for, or guess what it'll find.
- Request it to provide only confirmed, valuable findings over minor or unconfirmed ones. No findings are better than wrong ones.

Review and assess the results provided by the agent. Verify each finding it raises. They could be wrong or misled. Incorporate only what is valid and adds value (even if minor enhancements).

## Plugin Data Location Config

Unless specified otherwise, use the plugin data for where to find and save relevant plugin artifacts.
- **Plugin Data Path** — `${user_config.save_path}`, or `.spec-docs` if `save_path` isn't set. Create it if needed.
- **Feature folder** — `<plugin-data-path>/<feature-slug>`.
- **Feature slug** — 2–4 words, hyphenated. Before saving, check the existing folders under the plugin data path for any that clearly match (name and recency). Assume a new slug if none clearly match.
- **Save File Name** — `<feature-folder>/data-model.md`. Fixed, lowercase.

Unsure where it should go? Ask with the blocking-question tool (unless running autonomously). Otherwise assume the defaults and confirm the resolved path in the close.

## Writing style

- Write the doc and everything in chat to prioritize the reader's understanding — plain language, no jargon beyond the domain terms the model genuinely needs.
- Don't narrate the code-reading or your analysis as a frame; use it to shape the model.
- Explain what isn't obvious — the reader isn't looking at the code or your analysis.
- Keep questions for the user in their own section — don't bury them in prose.
- Reserve the blocking-question tool for mechanical decisions with clear answers; framing and judgment belong in conversation.
