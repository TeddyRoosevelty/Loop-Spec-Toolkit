# Conventions — spec card

The repo-wide rules a cold agent must follow to produce work that fits: what the project is and its stack, where things live, how to build and test, and the coding patterns and rules to follow. Extract the conventions the code actually follows, not generic best practice, and mark intended changes as intended.

**Template:** [../templates/conventions.md](../templates/conventions.md) · **Saves as:** `conventions.md`

## Ground in

Any existing conventions doc, `CLAUDE.md`, or contributing docs, and the repo's config — package manifests, lint and format setup, CI. Recap what the project is and how it's organized.

## Analysis method

Extract the conventions the code actually follows. Read across the codebase for the structure, the build and test commands, and the patterns and idioms work follows — sampling enough that the conventions are the real ones, not a guess. Hold what's followed today apart from what's an intended change. On a large repo, dispatch parallel search agents to sample patterns across it, then verify yourself.

## Drafting notes

Fill the overview and stack, the project structure, the commands, and the conventions. Add the testing, git, or pitfalls sections only when they carry something the core doesn't. Validate that the conventions match the real code — de-facto patterns, not generic best practice — that the commands actually run, named from the config rather than guessed, and that each rule is one a cold agent could follow.

## Facilitation angles

- Where the codebase is inconsistent, and which pattern should be the convention.
- Which rules actually prevent slop, against noise the agent doesn't need.
- What's worth changing versus documenting as-is.

## Standards

- **Grounded** — the conventions are extracted from the real code, the patterns it actually follows, not generic best practice.
- **Actionable** — each rule is one a cold agent could follow, concrete rather than aspirational.
- **Operational** — the build, test, and run commands are real and named from the config, not guessed.
- **Lean** — it carries the rules that keep work consistent and prevent slop, not a style encyclopedia.
- **Current and intended kept distinct** — what the code follows today is separated from proposed changes.

## Verify focus

Where the rules don't hold against the real code.

## Save note

If the user wants it to live at the repo's `CLAUDE.md` or `AGENTS.md`, or names a path, use that instead of the default location.
