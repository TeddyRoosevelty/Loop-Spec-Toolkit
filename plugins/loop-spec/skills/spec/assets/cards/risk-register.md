# Risk Register — spec card

The risks facing a body of work, each with its likelihood, impact, and a response, expanding to assumptions, issues, and dependencies when the work warrants the full RAID. Surface this work's real risks, not generic boilerplate, and give each one a response.

**Template:** [../templates/risk-register.md](../templates/risk-register.md) · **Saves as:** `risk-register.md`

## Ground in

The plan or requirements doc if one exists, and any existing register. An existing register gets its statuses updated and revisited with the user rather than rebuilt.

## Analysis method

Surface what could derail the work and how to respond:

- **Find risks across the angles** — technical (from the code: fragile areas, dependencies, integrations), product and delivery (from the user jobs and scope), and the assumptions the work rests on. Run a premortem on the work: assume it failed, and work backwards to what most plausibly caused it — the failures the plan reads right past are the ones worth naming.
- **Rate and respond** — for each real risk, assess its likelihood and impact and decide a response: mitigate, accept, avoid, or transfer.

## Drafting notes

Fill the scope, and the risk register — each risk with its likelihood, impact, and response, ranked by severity. Add the assumptions, issues, or dependencies sections when the work warrants the full RAID. Validate that each risk is specific to this work and traceable to something real, that each has a response, and that the register leads with the severe risks. The honest account names the uncomfortable risks worth not glossing over.

## Facilitation angles

- Whether the severe risks are the real ones, or something bigger is unnamed.
- Whether each response is enough, or just acknowledges the risk.
- Which assumptions, if wrong, would hurt the most.

## Standards

- **Specific** — each risk is this work's real exposure, traceable to the code, user jobs, or scope, not generic boilerplate.
- **Assessed** — each carries a likelihood and an impact, so the register can be ranked.
- **Actionable** — each has a response: mitigate, accept, avoid, or transfer — not just a statement of dread.
- **Ranked** — it leads with the severe risks (likelihood × impact), not the order they were found.
- **Honest** — the uncomfortable risks are named, not smoothed over.

## Verify focus

Where the risks, ratings, and responses don't hold when walked through.
