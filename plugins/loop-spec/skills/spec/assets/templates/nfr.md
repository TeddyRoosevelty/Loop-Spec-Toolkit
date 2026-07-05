# NFR Template

The artifact nfr writes: the quality attributes a system must meet, each as a measurable, verifiable target.

## Template

Replace every `{{token}}`; keep none.

```markdown
---
name: {{system_name}}
last_updated: {{YYYY-MM-DD}}
---

# {{system_name}} — Non-Functional Requirements

## Scope & conditions

{{What these targets cover, and the operating conditions they hold under — expected load, data volume, concurrency, environment.}}

## Quality targets

{{The non-functional requirements that matter, grouped by attribute — performance, scalability, reliability and availability, security, accessibility, observability, maintainability, compliance — including only the attributes that bear on this system. State each as a measurable threshold with the condition it holds under, how it's verified, and whether it's must-meet or aspirational. A table reads well here.}}

<!-- Conditional sections — add only when they carry something the above doesn't -->

## Current baseline

{{What the system does today on these attributes, where it's known — the ground the targets build from.}}

## Constraints & assumptions

{{The limits and givens the targets rest on — infrastructure budget, third-party SLAs, data residency.}}
```

## Guidelines

- Use the template's sections as-is — don't add top-level sections. Set `name` and the H1 to the system name, and `last_updated` to today's date on every write.
- Include only the quality attributes that bear on this system. An attribute with no real target is left out, not filled with a placeholder.
- State every target as a measurable threshold with the condition it holds under and how it's verified — a number, not an adjective.
- Mark proposed numbers as proposals until the user sets them; the targets are theirs to own.
- Match depth to the system — a small feature gets a few targets, not a full quality model.
- Write plainly, for a reader who isn't looking at the code. Domain language is fine where it's needed; invented jargon isn't.
