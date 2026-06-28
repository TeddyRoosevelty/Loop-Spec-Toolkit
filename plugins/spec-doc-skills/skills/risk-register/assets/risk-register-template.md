# Risk Register Template

The artifact risk-register writes: a living register of the risks facing a body of work — each with its likelihood, impact, and response — expandable to the full RAID.

## Template

Replace every `{{token}}`; keep none.

```markdown
---
name: {{topic}}
last_updated: {{YYYY-MM-DD}}
---

# {{topic}} — Risk Register

## Scope

{{What this register covers — the work, system, or timeframe — in a line or two.}}

## Risks

{{The risks facing the work, ranked by severity (likelihood × impact). One row each: the risk, its likelihood, its impact, and the response — mitigate, accept, avoid, or transfer.}}

| Risk | Likelihood | Impact | Response |
|------|------------|--------|----------|
| {{risk}} | {{low / med / high}} | {{low / med / high}} | {{the response}} |

<!-- Conditional sections — add only when they carry something the above doesn't -->

## Assumptions

{{Things taken as true that would become risks if they turn out wrong.}}

## Issues

{{Risks that have already materialized — active problems, with what's being done about them.}}

## Dependencies

{{External things the work relies on, and the exposure if they slip.}}
```

## Guidelines

- Use the template's sections as-is — don't add top-level sections. Set `name` and the H1 to the topic, and `last_updated` to today's date on every write.
- Lead with the severe risks — order by likelihood × impact, not the order they surfaced.
- Make each risk specific to this work and give it a response; a generic risk with no response earns no row.
- Add the Assumptions, Issues, or Dependencies sections only when the work warrants the full RAID; a register of just risks is fine.
- When revisiting, update the register in place — move materialized risks to Issues, and close the ones that have been mitigated.
- Write plainly, for a reader who isn't looking at the code or strategy. Domain language is fine where it's needed; invented jargon isn't.
