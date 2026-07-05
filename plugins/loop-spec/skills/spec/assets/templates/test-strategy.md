# Test Strategy Template

The artifact test-strategy writes: a risk-driven plan for proving a body of work correct — what to test, at which levels, the scenarios, and the bar for done.

## Template

Replace every `{{token}}`; keep none.

```markdown
---
date: {{YYYY-MM-DD}}
topic: {{kebab-case-topic}}
---

# Test Strategy: {{Title naming the work under test}}

## Scope

{{What's being tested, and what's deliberately out.}}

## Risks

{{What's most likely to break or most costly if it does — the areas that earn the deepest testing.}}

## Test approach

{{The levels used — unit, integration, end-to-end, manual, and any specialized ones — and what each must establish, with depth matched to the risks.}}

## Scenarios

{{The specific cases to verify, organized by dimension: happy path (core behavior), edge cases (boundaries, empty or null, concurrency), error paths (bad input, downstream failure, timeouts, permissions), and integration (what mocks alone can't prove).}}

## Coverage & done

{{What must be covered for the work to count as tested, the gaps left uncovered and why, and the bar that says testing is complete.}}

<!-- Conditional sections — add only when they carry something the above doesn't -->

## Environment & data

{{The framework, how and where tests run, and the fixtures or seed data they need.}}

## Specialized testing

{{Performance, security, accessibility, or load testing when the work warrants a distinct approach.}}
```

## Guidelines

- Keep the frontmatter exact — a later run uses it to name and find the file. Treat the body as a guide: carry a section when it adds something, drop it when it doesn't.
- Match depth to risk — a config change gets a line per section; a payment or auth flow gets a layered approach across several levels. The whole plan is risk-driven, not a flat checklist.
- Name the cases to verify and the level for each, not the test code. The plan says what must be proven and how it will be proven, and stops there.
- Be honest about coverage: name what's left uncovered and why, rather than implying everything is covered.
- Ground the levels and tooling in what the project actually has.
- Write plainly, for a reader who isn't looking at the code. Domain language is fine where it's needed; invented jargon isn't.
