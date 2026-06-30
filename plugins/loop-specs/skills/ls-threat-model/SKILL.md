---
description: Design a threat model — what's worth protecting in a system, how it could be attacked, and the mitigations that defend it, grounded in the real attack surface. Use when the user wants to analyze a system's security before it's exploited — "threat-model this", "what are the security risks for X" — rather than review a specific change for vulnerabilities.
argument-hint: "[the system or feature to threat-model]"
---

# Threat Model Designer

Draft and refine a threat model with the user — what's worth protecting in a system, the ways it could be attacked, and the mitigations that defend it. The bar every threat clears is in **Threat model standards** below; the steps reference it rather than restating it.

## Process

Read [assets/threat-model-template.md](assets/threat-model-template.md) up front — it's the artifact every step builds toward. Compress a step the work doesn't earn — acknowledge the skip rather than dropping it silently.

### 1. Ground in the system

Read any existing threat model and the data model if present. Settle the scope — the system, a feature, or a boundary — and recap what it does and what data it handles, then confirm before analyzing.

### 2. Analyze

Work the system from an attacker's view, and produce the analysis the draft is built from:

- **Map the attack surface** from the code — entry points, trust boundaries, auth, inputs, secrets, integrations.
- **Name the assets worth protecting** — the data, secrets, and capabilities an attacker would want.
- **Surface threats** against each asset, sweeping the STRIDE categories — spoofing, tampering, repudiation, information disclosure, denial of service, elevation of privilege.
- **Rate severity and decide a mitigation** for each, or name it as accepted residual risk.

Hold two disciplines while you work:

- **Work delegated surfaces — don't wave them away.** A surface a platform or third party handles — payments, auth, an external service — is still in scope. Particularly around the interfaces between systems. Name the trust anchor it rests on and verify it, or flag it as an unverified assumption.
- **Scale recon to the surface.** Read directly for a small one; for a large one, dispatch parallel search agents to map entry points, auth, and data handling, then verify yourself.

Run the adversary:
- Once the surface and assets are mapped and the threats rated, determine the riskiest areas, then dispatch a `loop-specs:threat-model-adversary` to work them.
- Own what it returns: re-trace each chain to real code, then fold in anything valid and valuable.

### 3. Propose

Shape the analysis into a draft, then check it holds.

#### Produce the draft

Fill the template from the analysis — the scope and assets, the attack surface, the rated and anchored threats, and their mitigations. Use a data-flow diagram where it shows the boundaries better than prose. Add a conditional section only when it carries something the core doesn't.

#### Validate

Run the draft against the **threat model standards** below — this is the gate before presenting. Walk each threat: anchored, assessed, and either mitigated by a real control or named as accepted residual risk; every asset threatened or cleared; every delegated surface resting on a named trust anchor. A threat that fails one isn't ready.

### 4. Present

Present the draft so the reader can follow it without the code in front of them.

#### The draft

Present the threat model — the best-effort analysis from what you found. It's both the first draft and the thing the user reacts to.

#### Honest account

Close with an honest read: where threats are grounded in the real surface, which rest on assumptions about how the system is deployed or used, and what residual risk is being accepted.

### 5. Facilitate

Surface the security decisions that actually matter — the ones your analysis exposed. Use the draft as something concrete to push against, but draw the questions from how the system is really exposed.

Be a thinking partner with small batches of questions, considering what the user leans toward before offering your read. Useful angles:

- Whether the highest-severity threats are the real ones, against how the system is actually exposed.
- Whether each mitigation is enough, or just names a control.
- Which residual risks are acceptable, and at what cost to close them.

The result can re-affirm the draft, reshape it, or reprioritize the threats. When a bigger exposure surfaces, rework it as a v2 and present it as such. Before capturing, reflect the settled shape back — the assets, the severe threats, their mitigations, and anything you'd flag. If the user revises, fold it in and re-confirm rather than writing straight away.

### 6. Capture

Save only when the user asks or confirms. Ask what's next with the blocking-question tool:

- **Refine in conversation (or stop here)** — no file written; the alignment carries forward in conversation.
- **Save** — write the threat model per the template and the plugin data location config below, with `last_updated` set to today.

## Threat model standards

The bar a threat model clears — the single source of truth for what "good" means here. The steps above check against it rather than re-spelling it. A strong model is:

- **Anchored** — each threat ties to a real asset and a real entry point in the code, not a generic checklist item.
- **Asset-driven** — what's worth protecting is named first, and every named asset is either threatened or explicitly cleared, so threats map to real loss and none is silently dropped.
- **Mitigated** — each threat has a concrete control, or is named as accepted residual risk. A control names what actually stops the threat ("reject requests that fail schema X at the gateway"), not the goal it serves ("validate input").
- **Assessed** — each threat carries a severity, so the model can be prioritized.
- **Honest about exposure** — assumptions about deployment and trust are stated, including the trust anchor any delegated surface rests on, and residual risk is named rather than implied away.

## Running autonomously

When asked to run autonomously, skip facilitation — but keep the threat-model-adversary on any non-trivial surface.

In facilitation's place, run the "Verify on request" step.

## Verify on request

When asked to verify the threat model.

Dispatch a new, general adversarial agent to review the draft, briefed to stress-test the threat model as written — its mitigations, severities, and coverage — to find where the model doesn't hold up by walking through it, rather than to hunt fresh attack chains.
- Don't bias on the results, tell it what to look for, or guess what it'll find.
- Request it to provide only confirmed, valuable findings over minor or unconfirmed ones. No findings are better than wrong ones.

Review and assess the results provided by the agent. Verify each finding it raises. They could be wrong or misled. Incorporate only what is valid and adds value (even if minor enhancements).

## Plugin Data Location Config

Unless specified otherwise, use the plugin data for where to find and save relevant plugin artifacts.
- **Plugin Data Path** — `${user_config.save_path}`, or `.loop-specs` if `save_path` isn't set. Create it if needed.
- **Feature folder** — `<plugin-data-path>/<feature-slug>`.
- **Feature slug** — 2–4 words, hyphenated. Before saving, check the existing folders under the plugin data path for any that clearly match (name and recency). Assume a new slug if none clearly match.
- **Save File Name** — `<feature-folder>/threat-model.md`. Fixed, lowercase.

Unsure where it should go? Ask with the blocking-question tool (unless running autonomously). Otherwise assume the defaults and confirm the resolved path in the close.

## Writing style

- Write the threat model and everything in chat to prioritize the reader's understanding — plain language, no jargon beyond the domain terms the analysis genuinely needs.
- Don't narrate the code-reading or your analysis as a frame; use it to shape the model.
- Explain what isn't obvious — the reader isn't looking at the code or your analysis.
- Keep questions for the user in their own section — don't bury them in prose.
- Reserve the blocking-question tool for mechanical decisions with clear answers; framing and judgment belong in conversation.
