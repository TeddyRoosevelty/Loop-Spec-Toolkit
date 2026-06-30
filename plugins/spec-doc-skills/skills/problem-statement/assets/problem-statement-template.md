# Problem Statement Template

The artifact problem-statement writes: a short, durable statement of one problem or opportunity worth solving — the problem, not a solution — grounded in evidence.

## Template

Replace every `{{token}}`; keep none.

```markdown
---
name: {{problem_name}}
last_updated: {{YYYY-MM-DD}}
---

# {{Problem name — names the problem, not the solution}}

## Problem

{{The situation and what's wrong or missing, in 1-3 sentences. No solution language.}}

## Who it affects

{{Who feels the problem and how — the primary group, and others when it matters.}}

## Evidence

{{The proof the problem is real and at the scale claimed: data, observed behavior, code, a user signal. What you saw first-hand, not an assertion.}}

## Impact & opportunity

{{The cost of leaving it unsolved, and the value unlocked by solving it — the two sides of why it matters.}}

## Why it's hard

{{The root cause and the crux — what keeps the problem in place, and why it isn't already solved.}}

## Desired outcome

{{What "solved" looks like, stated as outcomes a solution would have to produce — concrete enough to later tell whether it was reached. Not a solution.}}

<!-- Conditional sections — add only when they carry something the above doesn't -->

## Why now

{{The forcing function or window that makes this the moment.}}

## Out of scope

{{Adjacent problems deliberately set aside, so the statement stays on one.}}

## Constraints & assumptions

{{Known limits and the things taken as given.}}
```

## Guidelines

- Use the template's sections as-is — don't add top-level sections. Set `name` and the H1 to the problem name, and `last_updated` to today's date on every write.
- Match depth to the problem. A sharp, small problem gets a short statement — a section may be a single line. Drop a conditional section when it has nothing real to say; never leave an empty header or pad one with placeholder prose.
- Keep it solution-free. The problem and the desired outcome describe the need and what success looks like, never the thing to build — that belongs to the work downstream. The exception is a constraint that genuinely bounds the problem.
- Keep the desired outcome falsifiable: outcomes you could later check, not aspirations.
- Write plainly, for a reader who isn't looking at the code or your analysis. Domain language is fine where it's needed; invented jargon isn't.
