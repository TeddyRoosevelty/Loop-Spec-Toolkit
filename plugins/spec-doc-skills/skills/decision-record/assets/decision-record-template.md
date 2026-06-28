# Decision Record Template

The artifact decision-record writes: one significant decision — the context, the options, the choice, and the consequences.

## Template

Replace every `{{token}}`; keep none.

```markdown
---
status: {{proposed | accepted | superseded}}
date: {{YYYY-MM-DD}}
---

# {{NNNN}}. {{The decision, named — e.g. "Use Postgres for the primary store"}}

## Context

{{The forces, problem, and constraints that make this decision necessary.}}

## Options considered

{{The real alternatives weighed — each with its tradeoffs, fairly stated.}}

## Decision

{{The choice made, and why it wins over the alternatives.}}

## Consequences

{{What becomes easier and what becomes harder as a result — the tradeoffs accepted.}}

<!-- Conditional sections — add only when they carry something the above doesn't -->

## Related decisions

{{Decisions this supersedes, builds on, or constrains.}}
```

## Guidelines

- Keep the frontmatter exact — `status` and `date` drive the record's lifecycle. Set the H1 to the sequence number and the decision.
- Weigh genuine alternatives, fairly stated — a record with one real option and two strawmen records nothing.
- Name the harder consequences, not just the benefits; a decision with no downside is usually missing one.
- For a decision already made in the code, reconstruct the rationale and confirm it matches what the code does; mark reconstructed intent as such, and don't let hindsight make the choice look more inevitable than it was.
- Keep each record to one decision — a record covering several belongs split.
- Write plainly, for a reader who isn't looking at the code. Domain language is fine where it's needed; invented jargon isn't.
