# Task Brief Template

The artifact task-brief writes: the self-contained packet a cold agent reads to build one unit of work without asking.

## Template

Replace every `{{token}}`; keep none.

```markdown
---
date: {{YYYY-MM-DD}}
topic: {{kebab-case-topic}}
---

# Task Brief: {{Title naming the unit of work}}

## Task & scope

{{What to build, stated clearly, and what's in and out of scope for this unit.}}

## Context

{{The background the agent needs to build it right — why it matters and the situation around it — without overload.}}

## Starting points

{{The relevant files and where to work, and what to read first.}}

## Constraints & conventions

{{The patterns, standards, and boundaries the work must follow — including what not to touch.}}

## Acceptance & verification

{{What "done and correct" looks like, and how to confirm it — checks the agent can run or behavior it can observe on its own, not a bar only a human could judge.}}

<!-- Conditional sections — add only when they carry something the above doesn't -->

## Prerequisites

{{What must be in place before starting — other work, access, or setup.}}
```

## Guidelines

- Keep the frontmatter exact — a later run uses `date` and `topic` to name and find the file. Treat the body as a guide: carry a section when it adds something, drop it when it doesn't.
- Make it self-contained — a cold agent should be able to build it from the brief alone, without asking or guessing.
- Scope it to one unit a cold agent could land in one go; a brief covering a whole body of work belongs split.
- Say what to build and how to verify it — acceptance the agent can check itself — not the code; the implementation is the build's job.
- Keep the context to what the agent needs to build it right, not a full tour.
- Write plainly, for a reader who isn't looking at the code. Domain language is fine where it's needed; invented jargon isn't.
