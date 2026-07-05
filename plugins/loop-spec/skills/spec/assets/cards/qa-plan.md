# QA Plan — spec card

The concrete checks to run before shipping a change: the automated, manual, and exploratory verification, and the exit gate that says it's ready. Make each check runnable with a clear pass condition, and set an objective gate for shipping.

**Template:** [../templates/qa-plan.md](../templates/qa-plan.md) · **Saves as:** `qa-plan.md`

## Ground in

The plan or test strategy if one exists, and the codebase's test setup — suites, tools, CI. Settle what's being verified and how risky it is.

## Analysis method

Work out what to check before shipping and how. From the change and its risks, decide the checks — which automated suites to run, what to check manually, where to explore, what smoke tests to run after deploy. For each, settle how it's run and what passing looks like, and the existing behavior worth re-checking.

## Drafting notes

Fill the scope, the checks with how-to-run and pass conditions, and the exit criteria. Add the environments, regression, or entry-criteria sections when the change needs them. Validate that each check is concrete and runnable with a clear pass condition, the exit gate is objective, the regression areas for this change are covered, and the checks use the project's real suites and tools. The honest account names the riskiest area the plan leans on manual checking for.

## Facilitation angles

- Whether the checks actually cover the change's risks.
- What existing behavior could regress and isn't being re-checked.
- Whether the exit gate is objective enough to make a clean go/no-go.

## Standards

- **Runnable** — each check is concrete, with how to run it and what passing looks like, not "test the feature."
- **Gated** — the exit criteria are objective, so the ship decision is a clean go/no-go.
- **Regression-aware** — the existing behavior the change could break is named and re-checked.
- **Grounded** — the checks use the project's real suites, tools, and environments.
- **Honest** — what's left unverified is named, not implied away.

## Verify focus

Where the checks and exit gate don't hold when walked through.
