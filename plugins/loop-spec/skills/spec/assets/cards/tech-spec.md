# Tech Spec — spec card

The design for one piece of work: the approach, the components and flows it touches, the key decisions and the alternatives weighed, and the open questions. Design the approach and the rationale, not the code, and weigh genuine alternatives while keeping the unresolved honestly unresolved.

**Template:** [../templates/tech-spec.md](../templates/tech-spec.md) · **Saves as:** `tech-spec.md`

## Ground in

The requirements or problem doc if one exists, and any existing spec. Settle what's being designed — the feature, its goals and non-goals. Read the codebase for the patterns and prior art the design should fit.

## Analysis method

Work out the approach and the alternatives, grounded in the codebase:

- **Find the prior art** — the patterns, prior art, and components the work touches.
- **Settle the decisions and their alternatives** — the technical decisions the design forces, and the genuine alternatives for each.
- **Separate decided from deferred** — hold what's decided now apart from what implementation must discover.

**The design boundary:** a spec captures the approach, the decisions and their rationale, and the open questions. It doesn't contain implementation code or command scripts; short pseudo-code or a diagram is allowed only as direction, labeled as such. Don't run code to settle a design question — infer it from the codebase, or list it as an open question.

## Drafting notes

Fill the summary, goals and non-goals, the proposed design, the alternatives considered, and the risks and open questions. Add the detailed-design, cross-cutting, or dependencies sections only when the design needs them.

## Facilitation angles

- Whether the approach is the right one, or an alternative fits better than it first looked.
- Which open questions block building, and which can be settled in implementation.
- Where the design fights the codebase's existing patterns.

## Standards

- **Grounded** — the design fits the codebase's real patterns and prior art, not a greenfield ideal.
- **Weighed against real alternatives** — an alternative is genuine only if you can name a condition under which it would win.
- **Honest about the unresolved** — what's decided now is separated from what implementation must discover; open questions aren't papered over. A question blocks building when a wrong guess forces a rework; it can wait when it's reversible within the chosen approach.
- **Scoped** — goals and non-goals bound the design, so it doesn't sprawl.

## Verify focus

Where the design, its alternatives, and its claims don't hold against the codebase.
