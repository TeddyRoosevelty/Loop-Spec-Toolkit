# Threat Model — spec card

What's worth protecting in a system, the ways it could be attacked, and the mitigations that defend it — grounded in the real attack surface.

**Template:** [../templates/threat-model.md](../templates/threat-model.md) · **Saves as:** `threat-model.md`

## Ground in

Any existing threat model, and the data model if present. Settle the scope — the system, a feature, or a boundary — and what it does and what data it handles.

## Analysis method

Work the system from an attacker's view:

- **Map the attack surface** from the code — entry points, trust boundaries, auth, inputs, secrets, integrations.
- **Name the assets worth protecting** — the data, secrets, and capabilities an attacker would want.
- **Surface threats** against each asset, sweeping the STRIDE categories — spoofing, tampering, repudiation, information disclosure, denial of service, elevation of privilege.
- **Rate severity and decide a mitigation** for each, or name it as accepted residual risk.

Hold two disciplines: **work delegated surfaces — don't wave them away.** A surface a platform or third party handles — payments, auth, an external service — is still in scope, particularly the interfaces between systems; name the trust anchor it rests on and verify it, or flag it as an unverified assumption. And **scale recon to the surface** — on a large one, dispatch parallel search agents to map entry points, auth, and data handling, then verify yourself.

## Drafting notes

Fill the scope and assets, the attack surface, the rated and anchored threats, and their mitigations. Use a data-flow diagram where it shows the boundaries better than prose. Validate against the standards as the gate before presenting: walk each threat — anchored, assessed, and either mitigated by a real control or named as accepted residual risk; every asset threatened or cleared; every delegated surface resting on a named trust anchor. A threat that fails one isn't ready.

## Facilitation angles

- Whether the highest-severity threats are the real ones, against how the system is actually exposed.
- Whether each mitigation is enough, or just names a control.
- Which residual risks are acceptable, and at what cost to close them.

## Standards

- **Anchored** — each threat ties to a real asset and a real entry point in the code, not a generic checklist item.
- **Asset-driven** — what's worth protecting is named first, and every named asset is either threatened or explicitly cleared, so threats map to real loss and none is silently dropped.
- **Mitigated** — each threat has a concrete control, or is named as accepted residual risk. A control names what actually stops the threat ("reject requests that fail schema X at the gateway"), not the goal it serves ("validate input").
- **Assessed** — each threat carries a severity, so the model can be prioritized.
- **Honest about exposure** — assumptions about deployment and trust are stated, including the trust anchor any delegated surface rests on, and residual risk is named rather than implied away.

## Verify focus

Stress-test the model as written — its mitigations, severities, and coverage — where it doesn't hold up when walked through, rather than hunting fresh attack chains.
