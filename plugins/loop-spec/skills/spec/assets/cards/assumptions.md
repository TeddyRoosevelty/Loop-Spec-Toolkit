# Assumptions — spec card

The beliefs a piece of work takes as true and the bets it's making, each rated for how bad it would be if wrong and how sure we are, with a way to validate it. Surface the load-bearing assumptions — the ones that would sink the work if false — not just the safe and obvious ones.

**Template:** [../templates/assumptions.md](../templates/assumptions.md) · **Saves as:** `assumptions.md`

## Ground in

The requirements or plan doc if one exists, and any existing assumptions doc. Settle the work whose assumptions are being surfaced.

## Analysis method

Surface the beliefs the work rests on and how risky each is:

- **Invert what the plan takes as given.** For each thing it treats as settled, ask what must be true for it to hold. The beliefs that must hold but aren't proven are the load-bearing assumptions — the dangerous ones are those the work reads right past.
- **Separate known from assumed.** What's proven in the code or settled is a fact, not an assumption. Keep the two apart.
- **Rate each assumption** — how critical it is if false, how confident we are, and how it could be validated.

## Drafting notes

Fill the context, and the assumptions — each with its criticality, confidence, and how to validate it — ranked riskiest first. Add the hypotheses or validation-plan sections when the work has explicit bets to test. The risk ratings are proposals for the user to confirm. Validate that each item is genuinely an assumption, not an established fact; that the load-bearing ones are surfaced, not just the comfortable ones; and that the riskiest — critical and uncertain — lead. In the honest account, flag any high-confidence rating that rests on hope rather than evidence — those are the ones to confirm before locking in.

## Facilitation angles

- Which assumption, if wrong, would hurt the most — and whether it's been tested.
- Whether something listed as an assumption is actually known, or the reverse.
- Which leap-of-faith bets are worth validating before building.

## Standards

- **Genuinely assumptions** — each is a belief taken as true, not an established fact dressed up as one.
- **Load-bearing surfaced** — the risky, unstated assumptions are named, not just the safe obvious ones.
- **Rated** — each carries how critical it is if wrong and how confident we are, so the register can be ranked.
- **Testable** — each has a way it could be validated, even if that's "run a spike."
- **Ranked** — the critical-and-uncertain assumptions lead; the safe ones don't bury them.

## Verify focus

Stress-test the doc premortem-style: assume the work failed, and find the causing belief the doc missed or misrated.
