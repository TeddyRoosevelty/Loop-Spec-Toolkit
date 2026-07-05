# Data Model Template

The artifact data-model writes: the entities a system holds, their fields and relationships, and the rules that govern the data.

## Template

Replace every `{{token}}`; keep none.

```markdown
---
name: {{system_name}}
last_updated: {{YYYY-MM-DD}}
---

# {{system_name}} — Data Model

## Overview

{{What data the system holds and the model's scope.}}

## Entities

{{Each entity — its name and what it represents, its key, and its fields with their types and which are required.}}

## Relationships

{{How the entities relate — the cardinality (one-to-one, one-to-many, many-to-many) and the keys that link them. Use an ERD where it shows the structure better than prose.}}

## Constraints & invariants

{{The rules that govern the data — uniqueness, validation, referential integrity, and invariants that must always hold.}}

<!-- Conditional sections — add only when they carry something the above doesn't -->

## Lifecycle & state

{{The states a stateful entity moves through and the valid transitions between them.}}

## Enums & value sets

{{Shared enumerated values the entities reference.}}

## Storage & indexes

{{Where the data lives and the indexes that matter for how it's accessed.}}
```

## Guidelines

- Use the template's sections as-is — don't add top-level sections. Set `name` and the H1 to the system name, and `last_updated` to today's date on every write.
- Match depth to the model. A small domain gets a few entities — a section may be a single line. Drop a conditional section with nothing real to say; never leave an empty header or pad one with placeholder prose.
- Describe the real schema where one exists; mark proposed entities as proposed, kept distinct from what's defined.
- Keep it at the logical level — entities, fields, types, relationships, constraints — not migration SQL or ORM specifics.
- An ERD is authoritative content alongside the prose: include one where it shows structure prose can't, and keep the two consistent.
- Write plainly, for a reader who isn't looking at the code. Domain language is fine where it's needed; invented jargon isn't.
