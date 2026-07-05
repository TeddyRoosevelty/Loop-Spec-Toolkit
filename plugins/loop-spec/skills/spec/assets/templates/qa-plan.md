# QA Plan Template

The artifact qa-plan writes: the concrete checks to run before shipping a change, and the exit gate that says it's ready.

## Template

Replace every `{{token}}`; keep none.

```markdown
---
date: {{YYYY-MM-DD}}
topic: {{kebab-case-topic}}
---

# QA Plan: {{Title naming the change}}

## Scope

{{What's being verified, and what's out.}}

## Checks

{{The verification checks to run — automated suites, manual checks, exploratory areas, and post-deploy smoke tests. Each with how to run it and what passing looks like.}}

## Exit criteria

{{The gate that says it's verified and ready to ship — what must pass.}}

<!-- Conditional sections — add only when they carry something the above doesn't -->

## Environments

{{Where verification runs — staging, preview, production smoke.}}

## Regression areas

{{The existing behavior the change could affect, and what to re-check.}}

## Entry criteria

{{What must be ready before verification starts.}}
```

## Guidelines

- Keep the frontmatter exact — a later run uses `date` and `topic` to name and find the file. Treat the body as a guide: carry a section when it adds something, drop it when it doesn't.
- Make each check runnable — how to run it and what passing looks like, not "test the feature."
- Set objective exit criteria, so the ship decision is a clean go/no-go.
- Name the regression areas the change could break, and what to re-check.
- Ground the checks in the project's real suites, tools, and environments, and match depth to the risk.
- Write plainly, for a reader who isn't looking at the code. Domain language is fine where it's needed; invented jargon isn't.
