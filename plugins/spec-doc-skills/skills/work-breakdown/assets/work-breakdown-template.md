# Work Breakdown Template

The artifact work-breakdown writes: a body of work decomposed into discrete tasks, ordered by dependency.

## Template

Replace every `{{token}}`; keep none.

```markdown
---
date: {{YYYY-MM-DD}}
topic: {{kebab-case-topic}}
---

# Work Breakdown: {{Title naming the work}}

## Overview

{{The body of work being broken down, and its scope.}}

## Tasks

{{The work decomposed into discrete, trackable pieces — grouped where there's natural structure.}}

## Dependencies & sequence

{{What must come before what, and the order to tackle the tasks. Note where tasks can run in parallel.}}

<!-- Conditional sections — add only when they carry something the above doesn't -->

## Sizing

{{A rough, relative size per task — where it helps parcel the work.}}

## Phases & milestones

{{How the tasks group into phases or milestones.}}
```

## Guidelines

- Keep the frontmatter exact — a later run uses `date` and `topic` to name and find the file. Treat the body as a guide: carry a section when it adds something, drop it when it doesn't.
- Cover the whole work with no gaps, and keep each task discrete — a task that hides several belongs split.
- Keep tasks at a trackable grain — not micro-steps, not so big they hide work.
- Get the dependencies right; the sequence must not put a task before what it needs.
- Keep sizing rough and relative — small, medium, large — not hours.
- Write plainly, for a reader who isn't looking at the code. Domain language is fine where it's needed; invented jargon isn't.
