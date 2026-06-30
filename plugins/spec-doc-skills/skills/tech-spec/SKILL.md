---
description: Design a technical spec (RFC) — the design for one piece of work: the approach, the components and flows it touches, the alternatives weighed, and the open questions, grounded in the codebase. Use when the user wants a reviewable design before building — "write a design doc for X", "draft an RFC" — rather than the build order of a plan or the whole system's architecture.
argument-hint: "[the feature or change to design — or a path to its requirements doc]"
---

# Tech Spec Designer

Draft and refine a technical spec with the user — the design for one piece of work: the approach, the components and flows it touches, the key decisions and the alternatives weighed, and the open questions. Design the approach and the rationale, not the code, and weigh genuine alternatives while keeping the unresolved honestly unresolved.

## Process

Read [assets/tech-spec-template.md](assets/tech-spec-template.md) up front — it's the artifact every step builds toward. Compress a step the work doesn't earn — acknowledge the skip rather than dropping it silently.

### 1. Ground in the work

Read the requirements or problem doc if one was pointed to, and any existing spec. Settle what's being designed — the feature, its goals and non-goals — and recap before designing. Read the codebase for the patterns and prior art the design should fit.

### 2. Analyze

Work out the approach and the alternatives, grounded in the codebase.

- **Find the prior art.** The patterns, prior art, and components the work touches.
- **Settle the decisions and their alternatives.** The technical decisions the design forces, and the genuine alternatives for each.
- **Separate decided from deferred.** Hold what's decided now apart from what implementation must discover.

Scale the method to the area: read directly for a small change; for a large or unfamiliar one, dispatch parallel search agents to map it, then verify the load-bearing findings yourself. Stay on the design side of the design boundary below, and test the result against the tech spec standards below before drafting.

### 3. Propose

Shape the analysis into a draft, then check it holds.

#### Produce the draft

Fill the template from the analysis: the summary, goals and non-goals, the proposed design, the alternatives considered, and the risks and open questions. Add the detailed-design, cross-cutting, or dependencies sections only when the design needs them, and match depth to the work.

#### Validate

Check the draft against the tech spec standards below — genuine alternatives, honest open questions, a design that fits the codebase's real patterns and prior art. 

### 4. Present

Present the draft so the reader can follow it without the code in front of them.

#### The draft

Present the design — the best-effort approach from what you found. It's both the first draft and the thing the user reacts to.

#### Honest account

Close with an honest read: where the design is solid and grounded, where it rests on assumptions, and which questions it leaves open for review.

### 5. Facilitate

Surface the design decisions that actually matter — this is where a spec earns its review. Use the draft as something concrete to push against, but draw the questions from the codebase, the alternatives, and anything the evaluator surfaced.

Be a thinking partner with small batches of questions, considering what the user leans toward before offering your read. Useful angles:

- Whether the approach is the right one, or an alternative fits better than it first looked.
- Which open questions block building, and which can be settled in implementation.
- Where the design fights the codebase's existing patterns.

The result can re-affirm the draft, reshape it, or land on a different approach. When the approach changes, rework the spec as a v2 and present it as such. Before capturing, reflect the settled shape back — the approach, the key decisions, the open questions, and anything you'd flag. If the user revises, fold it in and re-confirm rather than writing straight away.

### 6. Capture

Save only when the user asks or confirms. Ask what's next with the blocking-question tool:

- **Refine in conversation (or stop here)** — no file written; the alignment carries forward in conversation.
- **Save** — write the spec per the template and the plugin data location config below.

## The design boundary

The line between designing the work and doing it. A spec captures the approach, the components and flows, the decisions and their rationale, and the open questions. It doesn't contain implementation code or command scripts; short pseudo-code or a diagram is allowed only as direction, labeled as such. Don't run code to settle a design question — infer it from the codebase, or list it as an open question.

## Tech spec standards

The bar a technical spec clears. A strong spec is:

- **Grounded** — the design fits the codebase's real patterns and prior art, not a greenfield ideal.
- **Weighed against real alternatives** — an alternative is genuine only if you can name a condition under which it would win. 
- **Honest about the unresolved** — what's decided now is separated from what implementation must discover; open questions aren't papered over. A question blocks building when a wrong guess forces a rework; it can wait when it's reversible within the chosen approach.
- **Scoped** — goals and non-goals bound the design, so it doesn't sprawl.

## Running autonomously

When asked to run autonomously, skip facilitation. 

Instead, run the "Verify on request" step.

## Verify on request

When asked to verify the spec.

Dispatch an adversarial agent to review the draft, briefed to stress-test the technical spec; to find where its design, its alternatives, and its claims don't hold by walking through it. 
- Don't bias on the results, tell it what to look for, or guess what it'll find. 
- Request it to provide only confirmed, valuable scenarios over minor or unconfirmed ones. No scenarios are better than wrong ones.

Review and assess the results provided by the agents. Verify each scenario and feedback it raises. They could be wrong or misled. Incorporate only what is valid and adds value (even if minor enhancements). 

## Plugin Data Location Config

Unless specified otherwise, use the plugin data for where to find and save relevant plugin artifacts.
- **Plugin Data Path** — `${user_config.save_path}`, or `.spec-docs` if `save_path` isn't set. Create it if needed.
- **Feature folder** — `<plugin-data-path>/<feature-slug>`.
- **Feature slug** — 2–4 words, hyphenated. Before saving, check the existing folders under the plugin data path for any that clearly match (name and recency). Assume a new slug if none clearly match.
- **Save File Name** — `<feature-folder>/tech-spec.md`. Fixed, lowercase.

Unsure where it should go? Ask with the blocking-question tool (unless running autonomously). Otherwise assume the defaults and confirm the resolved path in the close.

## Writing style

- Write the spec and everything in chat to prioritize the reader's understanding — plain language, no jargon beyond the domain terms the work genuinely needs.
- Don't narrate the code-reading or your analysis as a frame; use it to shape the design.
- Explain what isn't obvious — the reader isn't looking at the code or your analysis.
- Keep questions for the user in their own section — don't bury them in prose.
- Reserve the blocking-question tool for mechanical decisions with clear answers; framing and judgment belong in conversation.
