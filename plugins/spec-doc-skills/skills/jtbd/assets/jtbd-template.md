# JTBD Template

A JTBD doc — the main job the user hires the product for, the criteria they judge it by, and the concrete scenarios it should serve. The scenarios are the core: they help decide what to build next, so they stay concrete, while the job and criteria stay durable across feature changes.

## Template

Replace every `{{token}}`; keep none.

```markdown
---
name: {{product_name}}
last_updated: {{YYYY-MM-DD}}
---

# {{product_name}} — Jobs To Be Done & User Scenarios

## Main Job

{{When [situation], I want to [job], so I can [outcome]. Then a sentence or two of context.}}

### Related Jobs

- {{adjacent job the product also serves}}

### Emotional & Social Jobs

- {{how the user wants to feel, or to be seen, while doing the main job}}

## Success Criteria

{{Thematically grouped success criteria for the job — the yardsticks the user judges it done well by. Keep it light: observable yardsticks, not feelings.}}

## User Scenarios

{{6-8 concrete moments of the user succeeding with the app — the core of the doc. Each gives the real trigger (the user's own intent or words), what the user does, and what good looks like.}}

1. **{{Scenario name}}**
   {{The trigger (what the user is doing or saying) → what they do with the product → what good looks like.}}
```

## Guidelines

- Use the template's sections as-is — don't add top-level sections.
- Set `name` and the H1 title to the product name. Set `last_updated` to today's date on every write.
- Related jobs are named, not decomposed — they get no criteria or scenarios of their own.
- Emotional & social jobs are the feeling/perception layer of the main job, not separate jobs.
- Delete the Related Jobs or Emotional & Social Jobs section if there's nothing real to put there — never leave an empty header.
- Stay at the level of the job. Don't restate the problem, drift into metrics, or spec the solution or features.
- Keep the main job and criteria durable and solution-agnostic; let the scenarios be concrete and build-pointing.
- Keep success criteria at the job level — the user's own yardsticks — not the product's feature list or metrics. Naming current capabilities there dates the doc and turns the job into a checklist; the job shouldn't move when the feature list does.
- Scenarios should be concrete — name the real trigger and what serves it. The subject is the user's moment, not a feature tour, but don't strip the specifics that make it actionable.
- Keep it clear and easy to understand with traditional language choices. Avoid metaphors and jargon. Domain specific language is reasonable and necessary for clear communication, but do not invent our own. 
- If there is more than one user, distinguish them appropriately in the scenarios, etc.

## Tips
Tips for a well defined JTDB doc include (but not limited to):
- frames the main job around the end user's progress, durable across feature changes
- sets criteria that are the user's own observable yardsticks rather than product or feature metrics
- grounds scenarios in concrete moments of the user succeeding, specific enough to build toward.

Put the weight on the scenarios — make each concrete: the real trigger, what the user does, and what good looks like. Keep the criteria section light; it restates the job and isn't where the value is.

