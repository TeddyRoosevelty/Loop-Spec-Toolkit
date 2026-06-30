---
description: Design a non-functional requirements spec — the quality bars a system must meet for performance, reliability, security, accessibility, and the like, turned into measurable, verifiable targets. Use when the user wants to set or document quality targets — "what are our performance targets", "write the NFRs for X" — rather than the functional requirements of what the system does.
argument-hint: "[the system or feature to set quality targets for]"
---

# NFR Designer

Draft and refine a non-functional requirements spec with the user — the quality attributes a system must meet, each as a target with the condition it holds under and how it's verified. Turn vague quality wishes into measurable numbers a build can be designed and checked against.

## Process

Read [assets/nfr-template.md](assets/nfr-template.md) up front — it's the artifact every step builds toward. Compress a step the work doesn't earn — acknowledge the skip rather than dropping it silently.

### 1. Ground in the system

Read any existing NFR spec, and ground in the users, goals, and scenarios that point to which qualities matter. Settle which system or feature the targets cover and the conditions that matter — expected load, data volume, environment. Recap which quality attributes are in play and confirm the scope before setting targets.

### 2. Analyze

Work out which quality attributes actually matter for this system and what realistic targets look like.

- **Identify the attributes that bear on it.** From the user scenarios and the system's purpose — a real-time product leans on latency, a regulated one on security and compliance.
- **Find the current baseline.** Read the code and config for what the stack does today, so targets are grounded, not plucked. Infer the baseline from code, config, and known behavior rather than running the system to measure it.
- **Propose a target for each.** A sensible number per attribute that matters, knowing the user sets the real one.

Test the result against the NFR standards below before drafting.

### 3. Propose

Shape the analysis into a draft, then check it holds.

#### Produce the draft

Fill the template from the analysis: the scope and conditions, and the quality targets grouped by attribute — each a measurable threshold with its condition, how it's verified, and whether it's must-meet or aspirational. A table reads well for the targets. Add a conditional section only when it carries something the core doesn't.

#### Validate

Check that every target is measurable — a number or threshold, not an adjective — states the condition it holds under, and names how it's verified. Confirm the targets are realistic for the stack, and that proposed numbers are flagged as proposals for the user to set.

### 4. Present

Present the draft so the reader can follow it without the code in front of them.

#### The draft

Present the targets — the best-effort spec from what you found. It's both the first draft and the thing the user reacts to.

#### Honest account

Close with an honest read: where targets are grounded in the current baseline, where the numbers are proposals the user must own, and which attributes you judged not to matter for this system.

### 5. Facilitate

The numbers are the user's to set — surface the ones that matter. Use the draft as something concrete to push against, but draw the questions from what the product actually needs and the stack's real limits.

Be a thinking partner with small batches of questions, considering what the user leans toward before offering your read. Useful angles:

- Whether each target is set at the right level for what the product actually needs.
- Which attributes are must-meet versus nice-to-have.
- Where a target is more aspirational than the stack can realistically hit.

The result can re-affirm the draft, reshape it, or reset the targets. When the priorities reframe, rework the spec as a v2 and present it as such. Before capturing, reflect the settled shape back — the attributes that matter, their targets, and anything you'd flag. If the user revises, fold it in and re-confirm rather than writing straight away.

### 6. Capture

Save only when the user asks or confirms. Ask what's next with the blocking-question tool:

- **Refine in conversation (or stop here)** — no file written; the alignment carries forward in conversation.
- **Save** — write the spec per the template and the plugin data location config below, with `last_updated` set to today.

## NFR standards

The bar a non-functional requirement clears. A strong target is:

- **Measurable** — a number or threshold, not an adjective; "p95 under 200ms," not "fast."
- **Conditional** — it states the load, data volume, or environment it holds under.
- **Verifiable** — it names how the target is checked.
- **Grounded** — it's realistic for the stack and tied to a real need, not plucked or aspirational by default.
- **Prioritized** — must-meet targets are distinguished from aspirational ones.

## Running autonomously

When asked to run autonomously, skip facilitation.

Instead, run the "Verify on request" step.

## Verify on request

When asked to verify the spec.

Dispatch an adversarial agent to review the draft, briefed to stress-test the NFR spec; to find where its targets and the conditions they hold under don't stand up by walking through it.
- Don't bias on the results, tell it what to look for, or guess what it'll find.
- Request it to provide only confirmed, valuable findings over minor or unconfirmed ones. No findings are better than wrong ones.

Review and assess the results provided by the agent. Verify each finding it raises. They could be wrong or misled. Incorporate only what is valid and adds value (even if minor enhancements).

## Plugin Data Location Config

Unless specified otherwise, use the plugin data for where to find and save relevant plugin artifacts.
- **Plugin Data Path** — `${user_config.save_path}`, or `.loop-specs` if `save_path` isn't set. Create it if needed.
- **Feature folder** — `<plugin-data-path>/<feature-slug>`.
- **Feature slug** — 2–4 words, hyphenated. Before saving, check the existing folders under the plugin data path for any that clearly match (name and recency). Assume a new slug if none clearly match.
- **Save File Name** — `<feature-folder>/nfr.md`. Fixed, lowercase.

Unsure where it should go? Ask with the blocking-question tool (unless running autonomously). Otherwise assume the defaults and confirm the resolved path in the close.

## Writing style

- Write the spec and everything in chat to prioritize the reader's understanding — plain language, no jargon beyond the domain terms the system genuinely needs.
- Don't narrate the code-reading or your analysis as a frame; use it to shape the targets.
- Explain what isn't obvious — the reader isn't looking at the code or config.
- Keep questions for the user in their own section — don't bury them in prose.
- Reserve the blocking-question tool for mechanical decisions with clear answers; framing and judgment belong in conversation.


## Argument Flags
If the user arguments includes any of the following flags, follow them as if they are additional instructions:
--save, --autoSave: Once finalized, save the document in the save set without prompting
--autonomous, --auto: Run in autonomous mode. (see: "Running autonomously")
--verify: Run the "Verify on request" step.
