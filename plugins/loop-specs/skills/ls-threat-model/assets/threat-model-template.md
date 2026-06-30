# Threat Model Template

The artifact threat-model writes: a security analysis of a system — its assets, attack surface, threats, and mitigations.

## Template

Replace every `{{token}}`; keep none.

```markdown
---
name: {{topic}}
last_updated: {{YYYY-MM-DD}}
---

# {{topic}} — Threat Model

## Scope & assets

{{The system or feature under analysis, and what's worth protecting — the data, secrets, and capabilities an attacker would want. Note what was examined and what is assumed or left unexamined, so the file doesn't read as more complete than the analysis behind it.}}

## Attack surface

{{The trust boundaries and entry points where untrusted input or actors reach the system — endpoints, user inputs, auth boundaries, integrations. Use a data-flow diagram where it shows the boundaries better than prose.}}

## Threats

{{The ways the system could be attacked, each anchored to an asset and an entry point and rated for severity. Work the categories — spoofing, tampering, repudiation, information disclosure, denial of service, elevation of privilege. A table reads well.}}

## Mitigations

{{The controls that defend against each threat — those already in place and those still needed.}}

<!-- Conditional sections — add only when they carry something the above doesn't -->

## Trust model & assumptions

{{What the analysis treats as trusted — the platform, certain actors — and the assumptions it rests on.}}

## Residual risk

{{The risks accepted after mitigation, and why.}}
```

## Guidelines

- Use the template's sections as-is — don't add top-level sections. Set `name` and the H1 to the topic, and `last_updated` to today's date on every write.
- Anchor every threat to a real asset and entry point in the code; a generic checklist item with no anchor earns no place.
- Give each threat a mitigation or name it as accepted residual risk — a threat model is not just a list of fears.
- Rate each threat's severity so the model can be prioritized.
- Match depth to the surface — a small feature gets a focused model, not a full STRIDE matrix.
- Write plainly, for a reader who isn't looking at the code. Domain language is fine where it's needed; invented jargon isn't.
