# Strategy Template

The artifact strategy writes: a short, durable `STRATEGY.md`, filled from the interview's captured answers in the user's own words.

## Template

Replace every `{{token}}`; keep none.

```markdown
---
name: {{product_name}}
last_updated: {{YYYY-MM-DD}}
---

# {{product_name}} Strategy

## Target problem

{{1-2 sentence diagnosis: the user situation and the crux that makes it hard. No solution language.}}

## Our approach

{{1-2 sentence guiding policy: what this product commits to, so the problem becomes tractable.}}

## Who it's for

**Primary:** {{Persona}} — {{one-sentence job they're hiring the product to do}}

## Key metrics

- **{{metric name}}** — {{one-line definition; where it's measured}}

<!-- 3-5 total. -->

## Tracks

### {{Track name}}

{{One line: the investment area, not a feature list.}}

_Why it serves the approach:_ {{one line}}

<!-- 2-4 tracks. If you can't keep it to 4, fold related ones together. -->

<!-- Optional sections — delete any that weren't filled in -->

## Milestones

- **{{YYYY-MM-DD}}** — {{milestone}}

<!-- Externally visible only. -->

## Not working on

- {{one line per item}}

## Marketing

**One-liner:** {{single-sentence pitch}}

**Key message:** {{2-3 lines if useful}}
```

## Guidelines

- Use the template's sections as-is — don't add top-level sections.
- Delete any optional section (Milestones, Not working on, Marketing) that wasn't filled in — never leave an empty header.
- Set `name` in the frontmatter and the H1 title to the same product or initiative name. Set `last_updated` to today's date on every write.
