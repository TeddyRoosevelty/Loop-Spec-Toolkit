---
description: Design a glossary — the domain terms a project uses and their precise definitions, so the team and a cold agent use words consistently, extracted from the real code and docs. Use when the user wants a shared vocabulary — "write our glossary", "define the domain terms" — rather than the data model that structures the entities behind them.
argument-hint: "[the domain or repo to build the vocabulary for — defaults to the current repo]"
---

# Glossary Designer

Draft and refine a glossary with the user — the domain terms a project uses and their precise definitions, so the team and a cold agent use words the same way. Define the terms the code and domain actually use, and rule on the ones used inconsistently.

## Process

Read [assets/glossary-template.md](assets/glossary-template.md) up front — it's the artifact every step builds toward. Compress a step the work doesn't earn — acknowledge the skip rather than dropping it silently.

### 1. Ground in the domain

Read any existing glossary and the codebase's identifiers, models, and docs. Settle the domain the vocabulary covers and recap its shape, then confirm the scope before drafting.

### 2. Analyze

Harvest the terms that matter and how the code actually uses them. Read across the identifiers, models, and docs for the domain terms, their meanings, and where the same concept goes by several names or one name means two things. Keep to the terms that carry meaning, not every noun.

Scale the method to the domain: read directly for a small one; for a large one, dispatch parallel search agents to harvest terms across the code, then verify yourself. Test the result against the glossary standards below before drafting.

### 3. Propose

Shape the harvested terms into a draft, then check it holds.

#### Produce the draft

Fill the template from the analysis: the scope, and the terms — each with a precise definition, its aliases, and what it's distinct from where confusion is likely. Add the contested-terms section when usage conflicts and a canonical meaning is worth ruling. Group terms by area when the set is large.

#### Validate

Check that each term is real and its definition matches how the code uses it — not a vague gloss or an invented term — and that the disambiguations are accurate.

### 4. Present

Present the draft so the reader can follow it without the code in front of them.

#### The draft

Present the glossary — the best-effort vocabulary from what you found. It's both the first draft and the thing the user reacts to.

#### Honest account

Close with an honest read: where definitions match clear usage, where the code is inconsistent and you chose a canonical meaning, and any term you couldn't pin down.

### 5. Facilitate

Surface the decisions that actually matter — the ones your analysis exposed. Use the draft as something concrete to push against, but draw the questions from how the terms are really used.

Be a thinking partner with small batches of questions, considering what the user leans toward before offering your read. Useful angles:

- Which overloaded terms need a canonical ruling, and what it should be.
- Whether a definition distinguishes the term, or just restates it.
- Which terms actually carry meaning worth defining, against noise.

The result can re-affirm the draft, reshape it, or settle the contested terms. When a canonical meaning changes, rework the affected entries and re-present what changed. Before capturing, reflect the settled shape back — the key terms, the rulings made, and anything you'd flag. If the user revises, fold it in and re-confirm rather than writing straight away.

### 6. Capture

Save only when the user asks or confirms. Ask what's next with the blocking-question tool:

- **Refine in conversation (or stop here)** — no file written; the alignment carries forward in conversation.
- **Save** — write the glossary per the template and the plugin data location config below, with `last_updated` set to today.

## Glossary standards

The bar a glossary clears. A strong glossary is:

- **Grounded** — every term is one the code or domain actually uses, not invented.
- **Precise** — each definition distinguishes the term from its neighbors, not a vague gloss.
- **Disambiguated** — aliases and easily-confused terms are named where confusion is likely.
- **Canonical** — a term the code uses inconsistently gets one ruling, not several definitions.
- **Lean** — it defines the terms that carry meaning, not every noun in the codebase.

## Running autonomously

When asked to run autonomously, skip facilitation.

Instead, run the "Verify on request" step.

## Verify on request

When asked to verify the glossary.

Dispatch an adversarial agent to review the draft, briefed to stress-test the glossary; to find where its definitions and disambiguations don't hold against how the code uses the terms by walking through it.
- Don't bias on the results, tell it what to look for, or guess what it'll find.
- Request it to provide only confirmed, valuable findings over minor or unconfirmed ones. No findings are better than wrong ones.

Review and assess the results provided by the agent. Verify each finding it raises. They could be wrong or misled. Incorporate only what is valid and adds value (even if minor enhancements).

## Plugin Data Location Config

Unless specified otherwise, use the plugin data for where to find and save relevant plugin artifacts.
- **Plugin Data Path** — `${user_config.save_path}`, or `.spec-docs/docs` if `save_path` isn't set. Create it if needed.
- **Glossary folder** — `<plugin-data-path>/glossary`.
- **Save File Name** — `<glossary-folder>/GLOSSARY.md`.
- **File name** — always `GLOSSARY.md`.

If the user scopes the glossary to a single domain or names a path, use that path instead.

## Writing style

- Write the glossary and everything in chat to prioritize the reader's understanding — plain language.
- Don't narrate the code-reading or your analysis as a frame; use it to shape the definitions.
- Explain what isn't obvious — the reader isn't looking at the code or your analysis.
- Keep questions for the user in their own section — don't bury them in prose.
- Reserve the blocking-question tool for mechanical decisions with clear answers; framing and judgment belong in conversation.
