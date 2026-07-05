# Architecture — spec card

A map of how a system is built: its major components and what each owns, how they interact and where data flows, the load-bearing technical decisions, and the stack. Describe the system as it is, and mark intended changes as intended.

**Template:** [../templates/architecture.md](../templates/architecture.md) · **Saves as:** `architecture.md`

## Ground in

Any existing architecture doc — what the system is for, so its load-bearing decisions stand out. Settle the scope: the whole system, one service, or a subsystem.

## Analysis method

Map the real structure from the code — start from the entry points, the module or package boundaries, and the build and deploy config, then work inward:

- **Components and ownership** — the components and what each owns.
- **Interactions and data flow** — how they interact and where data flows.
- **The decisions that shaped it** — why the structure is the way it is.
- **Actual, not intended** — hold what the code actually does apart from what it's intended to become.

On a large or unfamiliar system, dispatch one exploration agent per subsystem or surface, then integrate their maps and verify the load-bearing structure against the source yourself.

## Drafting notes

Fill the overview and boundary, the components and responsibilities, how it fits together, the key decisions, and the stack. Use a diagram where it shows the structure better than prose. Validate by verifying components, boundaries, and data flow against the source — the real system, not an idealized one — and confirm anything aspirational reads as intended.

## Facilitation angles

- Whether the boundaries are drawn where they actually fall, or where they should.
- Which decisions are load-bearing enough to record, and whether their rationale still holds.
- Where current structure and intended direction diverge.

## Standards

- **Accurate to the code** — components, boundaries, and flows match what's actually there, verified rather than assumed.
- **At the right altitude** — structural: components, responsibilities, and interactions, not a file-by-file or line-level tour.
- **Current and intended kept distinct** — what is, stated as fact; what's planned, marked as intended.
- **Decisions carry their why** — each load-bearing choice records the reasoning, so a later change can tell whether it still holds.
- **Diagrams earn their place** — a diagram is there because it shows structure prose can't, and it stays consistent with the prose.

## Verify focus

Where the components, boundaries, and data flow don't hold against the code.
