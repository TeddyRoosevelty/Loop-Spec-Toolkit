# Architecture Template

The artifact architecture writes: a durable map of how a system is built — its components, how they fit together, the load-bearing decisions, and the stack.

## Template

Replace every `{{token}}`; keep none.

```markdown
---
name: {{system_name}}
last_updated: {{YYYY-MM-DD}}
---

# {{system_name}} — Architecture

## Overview

{{What the system is and does, in a short paragraph, and its boundary — what's inside it and the external systems or users it talks to.}}

## Components

{{The major building blocks, each with what it owns and is responsible for — one per entry.}}

## How it fits together

{{How the components interact and where data flows between them — the key paths through the system. Use a diagram (component, container, or sequence) where it shows the structure better than prose.}}

## Key decisions

{{The load-bearing architectural choices and the reasoning behind each — the ones a change must stay consistent with.}}

## Technology stack

{{The languages, frameworks, datastores, and infrastructure the system is built on.}}

<!-- Conditional sections — add only when they carry something the above doesn't -->

## Architectural drivers

{{The quality attributes and constraints that shaped the design — performance, scale, security, or reliability targets that forced choices.}}

## Cross-cutting concerns

{{How concerns that span components are handled — authentication, error handling, configuration, logging, observability.}}

## Runtime & deployment

{{How the system runs and deploys — processes, topology, environments.}}

## Risks & tradeoffs

{{Known weak points in the structure and what was traded for what.}}
```

## Guidelines

- Use the template's sections as-is — don't add top-level sections. Set `name` and the H1 to the system name, and `last_updated` to today's date on every write.
- Match depth to the system. A small service gets a short map — a section may be a single line. Drop a conditional section with nothing real to say; never leave an empty header or pad one with placeholder prose.
- Describe the system as it is. Mark anything aspirational as intended, kept distinct from the current structure.
- Keep it structural — components, responsibilities, interactions — not a file-by-file tour or implementation detail.
- A diagram is authoritative content alongside the prose: include one where it shows structure prose can't, and keep the two consistent.
- Write plainly, for a reader who isn't looking at the code or your analysis. Domain language is fine where it's needed; invented jargon isn't.
