# Requirements Document Template

The artifact requirements writes when a chosen direction is worth keeping: plain language, the decisions only, none of the process that produced them.

## Template

```markdown
# <Title — naming the proposed thing>

## Problem Statement

[The situation and cost that motivate the work: what's wrong or missing today, and
who it affects.]

## Objectives

[What success looks like, stated as the outcomes the work should achieve rather than
the features that achieve them.]

## Who it's for

[The people or systems the work serves; the primary audience.]

## In Scope

[What this work includes.]

## Out of Scope

[What it deliberately leaves out, including tempting non-goals worth naming.]

## Requirements

[What must be true about the proposed thing, as a plain bulleted list. When the
requirements span distinct concerns, group them under bold inline headers.]

## Acceptance Criteria

[The conditions that decide whether the work is done and correct: the checks a
reviewer or test can verify.]

<!-- Conditional sections — add only when they carry something the above doesn't -->

## Key Flows

[The multi-step behavior, with bold leader labels — **Trigger**, **Steps**,
**Outcome**. Add for behavioral work; usually reads best near Requirements.]

## Outstanding Questions

[Unresolved items, split into those that block planning and those that can be
answered during it.]
```

## Guidelines

- Write a doc only when the direction produced durable decisions worth keeping — scope, behavioral conditions, acceptance criteria a planner will need. A one-line decision needs no doc; a multi-step feature with contested scope does.
- Match depth to the work. A sparse direction gets a sparse doc — a section may be a single line. Keep the backbone: drop a section only when it genuinely has nothing to say, and never pad one with placeholder prose.
- Keep engineering-process exhaust out: no "captured at phase X" notes, no next-steps pointers.
- Keep implementation detail out by default — libraries, schemas, endpoints, and file layouts belong to planning. The exception is when the work itself is the technical or architectural decision; then the load-bearing choices belong here, at a high level.
