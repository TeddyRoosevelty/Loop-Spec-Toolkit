---
description: Design an interface contract — the operations an API, service, module, or event surface exposes, with the request and response shapes, errors, and auth that consumers build against and the producer must honor, grounded in the real code. Use when the user wants to pin down or document an interface — "spec this API", "define the contract for X" — rather than map the whole system or plan one change.
argument-hint: "[the API, service boundary, module, or event surface to specify]"
---

# API Contract Designer

Draft and refine an interface contract with the user — the operations an API, service, module, or event surface exposes, and for each the request and response shapes, the errors, and the auth that callers build against and the producer must honor. Document the real interface where one exists, and mark proposed operations as proposed.

## Process

Read [assets/api-contract-template.md](assets/api-contract-template.md) up front — it's the artifact every step builds toward. Compress a step the work doesn't earn — acknowledge the skip rather than dropping it silently.

### 1. Ground in the interface

Read any existing contract or interface definition — what the interface is for and the consumer needs it must serve. Settle the scope — which operations, which surface — and whether you're documenting an existing interface or specifying a new one. Recap and confirm before specifying.

- No contract → specify the scoped surface in full, then facilitate.
- An existing contract → summarize what's there in a few lines, and work out with the user what to revisit.

### 2. Analyze

Map the real shape of the interface from the code, and what consumers depend on.

- **Read the shapes.** For each operation, its inputs, outputs, types, error paths, and auth — from routes, handlers, serializers, and type definitions.
- **Separate exposed from proposed.** Hold what the code actually exposes apart from what's only proposed.
- **Note the consumers.** Who depends on the interface and on what; it sets what a change can and can't break.

Scale the method to the surface: read the code directly for a small interface; for a large or sprawling one, dispatch parallel search agents to map the operations, then verify the load-bearing shapes against the source yourself. Test the result against the contract standards below before drafting.

### 3. Propose

Shape the read interface into a draft, then check it holds.

#### Produce the draft

Fill the template from the analysis: the overview and consumers, the shared conventions, each operation with its request, response, errors, and auth, and the data types they reference. Specify types concretely. Add a conditional section only when it carries something the core doesn't, and match depth to the interface.

#### Validate

Verify each operation and type against the source — fields, types, status codes, and error paths match the real implementation, with nothing invented or missed. For a new interface, confirm it's internally consistent: every referenced type is defined, and every operation has its request, response, and errors. Confirm proposed operations read as proposed.

### 4. Present

Present the draft so the reader can follow it without the code in front of them.

#### The draft

Present the contract — the best-effort specification from what you found. It's both the first draft and the thing the user reacts to.

#### Honest account

Close with an honest read: where the contract is verified against the code, where it rests on inference, what's existing versus proposed, and any operation whose error paths or types you couldn't fully pin down.

### 5. Facilitate

Surface the contract decisions that actually matter — the ones your analysis exposed. Use the draft as something concrete to push against, but draw the questions from the code and what consumers depend on.

Be a thinking partner with small batches of questions, considering what the user leans toward before offering your read. Useful angles:

- Whether the shapes fit what consumers actually need.
- Which changes would break existing consumers, and whether that's intended.
- Where the contract should guarantee behavior — idempotency, ordering, side effects — that the draft left implicit.

The result can re-affirm the draft, reshape it, or restructure the contract. When the shape reframes, rework it as a v2 and present it as such. Before capturing, reflect the settled shape back — the operations, their key shapes, what consumers depend on, and anything you'd flag. If the user revises, fold it in and re-confirm rather than writing straight away.

### 6. Capture

Save only when the user asks or confirms. Ask what's next with the blocking-question tool:

- **Refine in conversation (or stop here)** — no file written; the alignment carries forward in conversation.
- **Save** — write the contract per the template and the plugin data location config below, with `last_updated` set to today.

## Contract standards

The bar an interface contract clears. A strong contract is:

- **Complete** — every operation states its request, response, errors, and auth; no operation is half-specified.
- **Precise** — types and shapes are concrete (named types, fields, required versus optional), not "an object with the data."
- **Anchored to consumers** — it captures what callers depend on, so a change can be judged against what it would break.
- **Accurate or consistent** — for an existing interface, every shape matches the code; for a new one, every referenced type is defined and every operation is whole.
- **Evolution-aware** — the versioning approach and what counts as a breaking change are stated.

## Running autonomously

When asked to run autonomously, skip facilitation.

Instead, run the "Verify on request" step.

## Verify on request

When asked to verify the contract.

Dispatch an adversarial agent to review the draft, briefed to stress-test the contract; to find where its operations, shapes, and claims don't hold against the code by walking through it.
- Don't bias on the results, tell it what to look for, or guess what it'll find.
- Request it to provide only confirmed, valuable findings over minor or unconfirmed ones. No findings are better than wrong ones.

Review and assess the results provided by the agent. Verify each finding it raises. They could be wrong or misled. Incorporate only what is valid and adds value (even if minor enhancements).

## Plugin Data Location Config

Unless specified otherwise, use the plugin data for where to find and save relevant plugin artifacts.
- **Plugin Data Path** — `${user_config.save_path}`, or `.spec-docs` if `save_path` isn't set. Create it if needed.
- **Feature folder** — `<plugin-data-path>/<feature-slug>`.
- **Feature slug** — 2–4 words, hyphenated. Before saving, check the existing folders under the plugin data path for any that clearly match (name and recency). Assume a new slug if none clearly match.
- **Save File Name** — `<feature-folder>/api-contract.md`. Fixed, lowercase. One doc per feature, covering its interfaces.

Unsure where it should go? Ask with the blocking-question tool (unless running autonomously). Otherwise assume the defaults and confirm the resolved path in the close.

## Writing style

- Write the contract and everything in chat to prioritize the reader's understanding — plain language, no jargon beyond the domain terms the interface genuinely needs.
- Don't narrate the code-reading or your analysis as a frame; use it to shape the contract.
- Explain what isn't obvious — the reader isn't looking at the code or your analysis.
- Keep questions for the user in their own section — don't bury them in prose.
- Reserve the blocking-question tool for mechanical decisions with clear answers; framing and judgment belong in conversation.
