# Glossary — spec card

The domain terms a project uses and their precise definitions, so the team and a cold agent use words the same way. Define the terms the code and domain actually use, and rule on the ones used inconsistently.

**Template:** [../templates/glossary.md](../templates/glossary.md) · **Saves as:** `glossary.md`

## Ground in

Any existing glossary and the codebase's identifiers, models, and docs. Settle the domain the vocabulary covers.

## Analysis method

Harvest the terms that matter and how the code actually uses them. Read across the identifiers, models, and docs for the domain terms, their meanings, and where the same concept goes by several names or one name means two things. Keep to the terms that carry meaning, not every noun. On a large domain, dispatch parallel search agents to harvest terms across the code, then verify yourself.

## Drafting notes

Fill the scope, and the terms — each with a precise definition, its aliases, and what it's distinct from where confusion is likely. Add the contested-terms section when usage conflicts and a canonical meaning is worth ruling. Group terms by area when the set is large. Validate that each term is real and its definition matches how the code uses it — not a vague gloss or an invented term — and that the disambiguations are accurate.

## Facilitation angles

- Which overloaded terms need a canonical ruling, and what it should be.
- Whether a definition distinguishes the term, or just restates it.
- Which terms actually carry meaning worth defining, against noise.

## Standards

- **Grounded** — every term is one the code or domain actually uses, not invented.
- **Precise** — each definition distinguishes the term from its neighbors, not a vague gloss.
- **Disambiguated** — aliases and easily-confused terms are named where confusion is likely.
- **Canonical** — a term the code uses inconsistently gets one ruling, not several definitions.
- **Lean** — it defines the terms that carry meaning, not every noun in the codebase.

## Verify focus

Where the definitions and disambiguations don't hold against how the code uses the terms.
