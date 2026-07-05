# Assumptions Template

The artifact assumptions writes: the beliefs a piece of work rests on and the bets it's making, each rated for risk and with a way to validate it.

## Template

Replace every `{{token}}`; keep none.

```markdown
---
name: {{topic}}
last_updated: {{YYYY-MM-DD}}
---

# {{topic}} — Assumptions

## Context

{{The work these assumptions and bets underpin.}}

## Assumptions

{{The beliefs the work takes as true, ranked riskiest first. One row each: the assumption, how critical it is if wrong, the confidence in it, and how it could be validated.}}

| Assumption | Criticality | Confidence | How to validate |
|------------|-------------|------------|-----------------|
| {{assumption}} | {{low / med / high}} | {{low / med / high}} | {{how}} |

<!-- Conditional sections — add only when they carry something the above doesn't -->

## Hypotheses

{{The explicit bets, stated as testable predictions — "we believe X; we'll know we're right if Y."}}

## Validation plan

{{How and when to test the riskiest assumptions and hypotheses — riskiest first.}}
```

## Guidelines

- Use the template's sections as-is — don't add top-level sections. Set `name` and the H1 to the topic, and `last_updated` to today's date on every write.
- List genuine assumptions — beliefs taken as true — not established facts. If it's proven in the code or settled, it's not an assumption.
- Surface the load-bearing assumptions, the ones that would sink the work if wrong; don't fill the register with safe, obvious ones.
- Rank riskiest first — critical and uncertain at the top.
- Give each a way to validate, even if that's pointing to a spike; mark proposed risk ratings as proposals for the user to confirm.
- Write plainly, for a reader who isn't looking at the code. Domain language is fine where it's needed; invented jargon isn't.
