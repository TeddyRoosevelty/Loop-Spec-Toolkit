---
description: Design an architecture doc — a map of a system's components, how they fit together, the load-bearing decisions, and the stack, grounded in the real code. Use when the user wants to capture or rethink how a system is structured — "document the architecture", "map how this fits together" — rather than plan one change or record a single decision.
argument-hint: "[the system, service, or subsystem to map]"
---

# Architecture Designer

Draft and refine an architecture doc with the user — a map of how a system is built: its major components and what each owns, how they interact and where data flows, the load-bearing technical decisions, and the stack. Describe the system as it is, and mark intended changes as intended.

## Process

Read [assets/architecture-template.md](assets/architecture-template.md) up front — it's the artifact every step builds toward. Compress a step the work doesn't earn — acknowledge the skip rather than dropping it silently.

### 1. Ground in the system

Read any existing architecture doc to ground in what the system is for, so its load-bearing decisions stand out. Settle the scope — the whole system, one service, or a subsystem — and recap what it's for in a line or two, then confirm before mapping.

- No doc → map the scope in full, then facilitate.
- An existing doc → summarize what's there in a few lines, and work out with the user what to revisit.

### 2. Analyze

Map the real structure from the code.

- **Components and ownership.** The components and what each owns.
- **Interactions and data flow.** How they interact and where data flows.
- **The decisions that shaped it.** Why the structure is the way it is.
- **Actual, not intended.** Hold what the code actually does apart from what it's intended to become.

Scale the method to the system: read the code directly for a small or familiar one; for a large or unfamiliar one, dispatch parallel exploration agents — one per subsystem or surface — then integrate their maps and verify the load-bearing structure against the source yourself. Test the result against the architecture standards below before drafting.

### 3. Propose

Shape the mapped structure into a draft, then check it holds.

#### Produce the draft

Fill the template from the analysis: the overview and boundary, the components and their responsibilities, how it fits together, the key decisions, and the stack. Use a diagram where it shows the structure better than prose. Add a conditional section only when it carries something the core doesn't, and match depth to the system.

#### Validate

Verify the load-bearing structural claims against the source — components, boundaries, and data flow describe the real system, not an idealized one. Confirm anything aspirational reads as intended, not stated as current.

### 4. Present

Present the draft so the reader can follow it without the code or your analysis in front of them.

#### The draft

Present the map — the best-effort structure from what you found. It's both the first draft and the thing the user reacts to.

#### Honest account

Close with an honest read: where the map is verified against the code, where it rests on inference, and what's current versus intended.

### 5. Facilitate

Surface the structural decisions that actually change the map — the ones your analysis exposed. Use the draft as something concrete to push against, but draw the questions from the code.

Be a thinking partner with small batches of questions, considering what the user leans toward before offering your read. Useful angles:

- Whether the boundaries are drawn where they actually fall, or where they should.
- Which decisions are load-bearing enough to record, and whether their rationale still holds.
- Where current structure and intended direction diverge.

The result can re-affirm the draft, reshape it, or restructure the map. When the structure reframes, rework it as a v2 and present it as such. Before capturing, reflect the settled shape back — the components, how they fit together, the key decisions, and anything you'd flag. If the user revises, fold it in and re-confirm rather than writing straight away.

### 6. Capture

Save only when the user asks or confirms. Ask what's next with the blocking-question tool:

- **Refine in conversation (or stop here)** — no file written; the alignment carries forward in conversation.
- **Save** — write the doc per the template and the plugin data location config below, with `last_updated` set to today.

## Architecture standards

The bar an architecture doc clears. A strong map is:

- **Accurate to the code** — components, boundaries, and flows match what's actually there, verified rather than assumed.
- **At the right altitude** — structural: components, responsibilities, and interactions, not a file-by-file or line-level tour.
- **Current and intended kept distinct** — what is, stated as fact; what's planned, marked as intended.
- **Decisions carry their why** — each load-bearing choice records the reasoning, so a later change can tell whether it still holds.
- **Diagrams earn their place** — a diagram is there because it shows structure prose can't, and it stays consistent with the prose.

## Running autonomously

When asked to run autonomously, skip facilitation.

Instead, run the "Verify on request" step.

## Verify on request

When asked to verify the architecture doc.

Dispatch an adversarial agent to review the draft, briefed to stress-test the architecture; to find where its components, boundaries, and data flow don't hold against the code by walking through it.
- Don't bias on the results, tell it what to look for, or guess what it'll find.
- Request it to provide only confirmed, valuable findings over minor or unconfirmed ones. No findings are better than wrong ones.

Review and assess the results provided by the agent. Verify each finding it raises. They could be wrong or misled. Incorporate only what is valid and adds value (even if minor enhancements).

## Plugin Data Location Config

Unless specified otherwise, use the plugin data for where to find and save relevant plugin artifacts.
- **Plugin Data Path** — `${user_config.save_path}`, or `.loop-specs` if `save_path` isn't set. Create it if needed.
- **Feature folder** — `<plugin-data-path>/<feature-slug>`.
- **Feature slug** — 2–4 words, hyphenated. Before saving, check the existing folders under the plugin data path for any that clearly match (name and recency). Assume a new slug if none clearly match.
- **Save File Name** — `<feature-folder>/architecture.md`. Fixed, lowercase.

Unsure where it should go? Ask with the blocking-question tool (unless running autonomously). Otherwise assume the defaults and confirm the resolved path in the close.

## Writing style

- Write the doc and everything in chat to prioritize the reader's understanding — plain language, no jargon beyond the domain terms the system genuinely needs.
- Don't narrate the code-reading or your analysis as a frame; use it to shape the map.
- Explain what isn't obvious — the reader isn't looking at the code or your analysis.
- Keep questions for the user in their own section — don't bury them in prose.
- Reserve the blocking-question tool for mechanical decisions with clear answers; framing and judgment belong in conversation.


## Argument Flags
If the user arguments includes any of the following flags, follow them as if they are additional instructions:
--save, --autoSave: Once finalized, save the document in the save set without prompting
--autonomous, --auto: Run in autonomous mode. (see: "Running autonomously")
--verify: Run the "Verify on request" step.
