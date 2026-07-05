# Conventions Template

The artifact conventions writes: the repo-wide rules a cold agent must follow to produce work that fits.

## Template

Replace every `{{token}}`; keep none.

```markdown
---
name: {{repo_name}}
last_updated: {{YYYY-MM-DD}}
---

# {{repo_name}} — Conventions

## Overview & stack

{{What the project is, in a line or two, and what it's built with — languages, frameworks, datastores.}}

## Project structure

{{Where things live — the directory layout that matters, and where to add new code.}}

## Commands

{{How to build, test, run, and lint — the commands an agent needs to do and verify work.}}

## Conventions

{{The coding patterns, naming, and idioms work must follow, and the rules specific to this project.}}

<!-- Conditional sections — add only when they carry something the above doesn't -->

## Testing conventions

{{How tests are written and organized, and what's expected of them.}}

## Git & PR conventions

{{Branch, commit, and PR norms.}}

## Pitfalls

{{Non-obvious traps and what not to touch.}}
```

## Guidelines

- Use the template's sections as-is — don't add top-level sections. Set `name` and the H1 to the repo name, and `last_updated` to today's date on every write.
- Extract the conventions the code actually follows; where the code is inconsistent, pick the dominant pattern and note it. Don't document generic best practice the repo doesn't follow.
- Keep the commands real — named from the config, and runnable.
- Mark intended changes as intended, kept distinct from current practice.
- Keep it lean — the rules that prevent slop, not a style encyclopedia.
- Write plainly, for the agent that will follow it. Domain language is fine where it's needed; invented jargon isn't.
