# Test Strategy — spec card

How the correctness of a body of work gets proven: the risks worth testing for, the test levels and what each must establish, the scenarios to cover, and the bar that says it's tested enough. Drive coverage by risk, and prove behavior rather than that code ran.

**Template:** [../templates/test-strategy.md](../templates/test-strategy.md) · **Saves as:** `test-strategy.md`

## Ground in

The plan or requirements doc if one exists — carry its behavior, scope, and acceptance criteria forward. Read the codebase's existing test setup: framework, conventions, CI, and what's already covered.

## Analysis method

Work out what could go wrong and how to catch it:

- **Rank the risks by likelihood × impact.** Depth follows the ranking — areas high on both earn the deepest testing; areas low on both get a line. Likely-to-break signals: complexity, new or unfamiliar code, churn, thin existing coverage, anything stateful or concurrent. Costly-if-broken signals: money, auth and permissions, data integrity, irreversible actions, a wide user-facing blast radius.
- **For each risk, pick the level and the cases.** Cover the dimensions that apply — happy path, edge cases, error paths, integration. Choose the level by what a cheaper one can't prove: a higher level (integration, end-to-end) earns its cost only where a unit test can't pin the behavior down, like a contract across components or state that mocks would assume away.
- **If the work isn't testable as written, say what has to change first.** Untested legacy, no seam, hidden dependencies — name the seam or characterization test needed, rather than planning tests that can't be written.

On a large surface, dispatch parallel search agents to map the existing coverage and test setup, then verify yourself. Ground the approach in the repo's real test tooling.

## Drafting notes

Fill the scope, the risks, the test approach by level, the scenarios by dimension, and the coverage-and-done bar. Match depth to risk — a config change gets a line, a payment flow a layered approach. Validate the two things easiest to miss: no high-risk area is left with shallow or no coverage, and the approach uses the repo's real test tooling — no framework or level the project doesn't have or hasn't committed to adopting. Confirm the scenarios name what to verify, not the test code.

## Facilitation angles

- Whether the riskiest areas are getting the deepest testing.
- Where a level — integration, end-to-end — would prove something unit tests can't.
- Which gaps are acceptable to leave uncovered, against the cost of covering them.

## Standards

- **Risk-driven** — depth follows risk; the areas most likely to break or most costly get the most coverage, and trivial areas get a line.
- **Behavior-proving** — tests establish what the code does, not that lines executed; coverage numbers are not the goal.
- **At the right altitude** — it names the cases to verify and the level for each, not the test code itself.
- **Honest about gaps** — what's left uncovered is named and justified, not silently omitted.
- **Grounded in the real setup** — the levels and tooling are ones the project actually has or will adopt, not generic.

## Verify focus

Where the risk ranking and coverage don't hold — on high-risk work (auth, payments, data integrity), the production incident this plan would not catch.
