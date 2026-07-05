# NFR — spec card

The quality attributes a system must meet, each as a target with the condition it holds under and how it's verified. Turn vague quality wishes into measurable numbers a build can be designed and checked against. The numbers are the user's to set — proposals are flagged as proposals.

**Template:** [../templates/nfr.md](../templates/nfr.md) · **Saves as:** `nfr.md`

## Ground in

Any existing NFR spec, and the users, goals, and scenarios that point to which qualities matter. Settle which system or feature the targets cover and the conditions that matter — expected load, data volume, environment.

## Analysis method

Work out which quality attributes actually matter for this system and what realistic targets look like:

- **Identify the attributes that bear on it** — from the user scenarios and the system's purpose; a real-time product leans on latency, a regulated one on security and compliance.
- **Find the current baseline** — read the code and config for what the stack does today, so targets are grounded, not plucked. Infer the baseline rather than running the system to measure it.
- **Propose a target for each** — a sensible number per attribute that matters, knowing the user sets the real one.

## Drafting notes

Fill the scope and conditions, and the quality targets grouped by attribute — each a measurable threshold with its condition, how it's verified, and whether it's must-meet or aspirational. A table reads well for the targets. Validate that every target is measurable, conditional, and verifiable, realistic for the stack, and that proposed numbers are flagged as proposals. The honest account names which attributes you judged not to matter for this system.

## Facilitation angles

- Whether each target is set at the right level for what the product actually needs.
- Which attributes are must-meet versus nice-to-have.
- Where a target is more aspirational than the stack can realistically hit.

## Standards

- **Measurable** — a number or threshold, not an adjective; "p95 under 200ms," not "fast."
- **Conditional** — it states the load, data volume, or environment it holds under.
- **Verifiable** — it names how the target is checked.
- **Grounded** — it's realistic for the stack and tied to a real need, not plucked or aspirational by default.
- **Prioritized** — must-meet targets are distinguished from aspirational ones.

## Verify focus

Where the targets and the conditions they hold under don't stand up.
