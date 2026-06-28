# Tech Spec Template

The artifact tech-spec writes: the design for one piece of work — the approach, the alternatives, and the open questions.

## Template

Replace every `{{token}}`; keep none.

```markdown
---
date: {{YYYY-MM-DD}}
topic: {{kebab-case-topic}}
status: {{draft | accepted}}
---

# Tech Spec: {{Title naming the work}}

## Summary

{{What this proposes and the problem it solves, in a paragraph.}}

## Goals & non-goals

{{What the design must achieve, and what's explicitly out of scope.}}

## Proposed design

{{The approach — the components and interfaces it touches, the data and control flow, and the key technical decisions and why. Use a diagram where it shows the design better than prose.}}

## Alternatives considered

{{The other approaches weighed, each with why it wasn't chosen.}}

## Risks & open questions

{{What's uncertain, and what still needs deciding — separating what blocks building from what can be settled in implementation.}}

<!-- Conditional sections — add only when they carry something the above doesn't -->

## Detailed design

{{Deeper specifics the proposed design summary doesn't carry — data model and API changes, algorithms, error handling, edge cases.}}

## Cross-cutting concerns

{{How the design handles security, performance, observability, migration, or backward compatibility.}}

## Dependencies

{{What the work relies on — other systems, teams, or work in flight.}}
```

## Guidelines

- Keep the frontmatter exact — a later run uses `date` and `topic` to name and find the file. Treat the body as a guide: carry a section when it adds something, drop it when it doesn't.
- Design the approach and the rationale, not the code — short pseudo-code or a diagram is allowed as direction, labeled as such.
- Weigh genuine alternatives — an alternative counts only if you can name when it would win; if there's genuinely none, say so and name what forces the choice rather than inventing a loser to fill the section.
- Keep the open questions honest — separate what's decided now from what implementation must discover, rather than faking certainty.
- Ground the design in the codebase's real patterns and prior art, and match depth to the work.
- Write plainly, for a reader who isn't looking at the code. Domain language is fine where it's needed; invented jargon isn't.
