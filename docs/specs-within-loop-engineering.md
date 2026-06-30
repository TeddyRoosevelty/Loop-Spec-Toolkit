# Specs within Loop Engineering

**What this covers:** what a loop is, and where a spec sits inside one. By the end you should be able to say what job a spec does in a loop, what it cannot do, and how to tell a spec that helps from one that is dead weight.

This page is self-contained. It explains loop engineering from the start, so you do not need anything else open to follow it. "Spec" here means a written statement of intent and constraints — a problem statement, a requirements doc, an architecture decision, a set of rules the work must respect.

The one line to hold while you read: **tests prove the code works; a spec is about whether it is the right code. A loop with only the first can pass every test while building the wrong thing.**

---

## 1. What a loop is

For the last couple of years, getting work out of a coding agent meant doing it by hand: write a prompt, read what comes back, write the next prompt. You drive every step.

Loop engineering changes who drives. Instead of prompting the agent yourself, you build a small system that prompts it for you. That system finds the work, hands it to the agent, checks the result, writes down what happened, and decides what to do next — then runs on its own. A "loop" is that system. Each time it runs, the agent moves through the same few steps — find the work, plan the change, make it, check it, then finish or go around again. That repeating shape — work, check, fix, repeat — is what "loop" means.

Everything about loops comes back to two facts about how agents behave:

1. **The agent forgets everything between runs.** Each run starts with a blank memory. Nothing it learned last time carries over unless you saved it somewhere.
2. **The agent tends to call its own work done.** Left to grade itself, it is too generous. It will report success on work that is half-finished or wrong.

These two facts tell you where the work is. Memory and honest checking cannot come from the agent — it is bad at both. They have to be built into the system around it.

## 2. The loop and the harness are two different things

To place a spec, you first have to split the system in two:

- **The loop** is the system *around* many runs: what starts a run, where memory is saved, what counts as done, when to stop.
- **The harness** is the setup *within* a single run: the instructions, context, checks, and tools the agent has while it works.


|             | Loop                                   | Harness                                             |
| ----------- | -------------------------------------- | --------------------------------------------------- |
| **Scope**   | across many runs                       | inside one run                                      |
| **Answers** | when to run, what's done, when to stop | what the agent knows and is allowed to do right now |
| **Holds**   | trigger, memory file, stop condition   | instructions, context, checks, tools                |


A good loop on a poorly set-up agent still fails. A spec is part of the harness — it shapes what the agent knows and how its work is judged *within* a run. So the rest of this page is mostly about the harness.

## 3. The whole game is checking

Of the agent's two weaknesses, a spec speaks to the second one: the agent grades itself too kindly. The fix for that is a check — something other than the agent that can tell good work from bad.

But "a check" is not one thing. Checks come in a few kinds, and they do not all catch the same mistakes. Sorting them is what tells you what your loop is missing.

## 4. The four kinds of check

Sort every check on two questions:

- **When does it run?** *Before* the agent acts, so it guides the work — or *after* the agent acts, so it catches mistakes.
- **How does it work?** *By fixed rules* (fast and deterministic — linters, type checkers, tests) or *by judgment* (something reads the work and forms an opinion — a code review, a behavior check).

That gives four kinds:


|                           | By fixed rules                            | By judgment                           |
| ------------------------- | ----------------------------------------- | ------------------------------------- |
| **Before the agent acts** | type systems, linters, architecture rules | **specs, written constraints**        |
| **After the agent acts**  | test suites, coverage, mutation tests     | agent code reviewers, behavior checks |


No single kind is enough on its own. Each cell catches a class of mistake the others miss, so the empty cells in your own loop are your gaps. A spec lives in one specific cell: **before the agent acts, by judgment.** That position is the whole reason it matters, and it is what the next two sections unpack.

## 5. The gap a spec covers

Read the table by column and the split is clear. The fixed-rule checks — linters, type checkers, tests — answer one question well: *does the code work?* They run on their own and return an error when something is broken.

What they cannot answer is *is this the right thing to build?* A test confirms the code does what the test says. It cannot tell you the test, or the work, was aimed at the right target in the first place. That is a judgment, not a rule.

This is the failure a spec exists to prevent: **a loop with only after-the-fact rule checks, and no before-the-agent judgment check, can pass every test while building the wrong thing.** The tests go green. The work is still wrong, because nothing in the loop ever checked the direction — only the execution. The spec is the before-the-act judgment check that sets the direction the rule checks later confirm.

## 6. The two jobs a spec does in a loop

Inside the harness, a spec earns its place by doing two distinct jobs, one for each of the agent's weaknesses.


| Job                                                    | When it works   | The weakness it answers          |
| ------------------------------------------------------ | --------------- | -------------------------------- |
| Standing context the agent reads at the start of a run | Every run       | The agent forgets between runs   |
| A judgment check on direction, before code is written  | Before the work | The agent builds the wrong thing |


**As standing context.** Because the agent starts each run blind, a spec it reads first — what the project is, the conventions, the architecture decisions, the constraints — is how the work fits the project instead of guessing at it. This is the same role a good onboarding doc plays for a new engineer.

**As a before-the-work check.** Before code is written, the spec states what success means and what the work must not do. The plan can be measured against it before any code exists. This is the judgment check from the table — the one that guards direction rather than correctness.

## 7. Load-bearing, or complementary?

It is worth being exact about a spec's status, because it is easy to overstate.

The single most load-bearing part of a loop is an objective check that can fail on its own — a command that returns an error, like a failing test suite or a type checker. A spec is **not** that. A spec cannot exit with an error code; it does not fail a run by itself. So a spec does not replace the objective check, and a loop is not complete just because it has one.

But a spec is not optional decoration either. It is the only thing covering an entire class of failure — work that is built correctly and is still the wrong work. Nothing in the fixed-rule cells catches that.

The clean way to hold both facts:

- The load-bearing parts — saved memory, a check that fails on its own, a checker separate from the maker, a hard stop — keep the loop from **lying to you**: forgetting, grading itself, never stopping.
- The spec keeps the loop from **building the wrong thing well**.

Different jobs. A serious loop needs both.

## 8. What makes a spec work, and what makes it dead weight

A spec helps only when it is grounded. A spec tied to what is real - actual constraints, concrete success criteria something else could check the work helps produce work that fits. A spec that captured your judgements in areas that are ambigious or easy to interpret helps produce work that meets your expectations. A spec that is an abstract wish list gives the illusion of direction and leaves the agent to invent the details, which is how invented file paths and made-up APIs get in.

A practical test: write the "done" condition concretely enough that a separate checker could judge it, not just the author. "It should feel fast" is not a spec a check can use. "The page responds in under 200ms on the test dataset" is.

A spec also has to earn its tokens. Its weight should scale with how much judgment "done" requires:


| The work                                | What "done" means                          | Spec weight                           |
| --------------------------------------- | ------------------------------------------ | ------------------------------------- |
| Deterministic cleanup (fix lint errors) | A rule check fully captures it             | Little or none — the test is the spec |
| Ambiguous feature work                  | A judgment call no single command captures | Heavy — the spec is doing real work   |


When one objective command already captures "good," that command is your real check and a heavy spec on top of it is dead weight. Keep the spec that is paying for itself, and no more.

## 9. Takeaways

- A loop is a system that prompts the agent for you and checks the result. It exists because the agent forgets between runs and grades itself too kindly.
- The loop is the system around many runs; the harness is the setup within one run. A spec is part of the harness.
- Sort checks by *when* they run (before/after the agent acts) and *how* (fixed rules vs. judgment). A spec is the before-the-act, by-judgment check. The empty cells in that grid are your gaps.
- Fixed-rule checks answer *does it work?* A spec answers *is it the right thing?* A loop with only the first can pass every test while building the wrong thing.
- A spec does two jobs: standing context the agent reads each run, and a before-the-work check on direction.
- A spec is not the load-bearing check — it cannot fail a run on its own — but it is the only cover for "wrong thing, built correctly." The load-bearing parts stop the loop from lying to you; the spec stops it from building the wrong thing well.
- A spec works only when it is grounded and its "done" condition is concrete enough for someone other than the author to judge. Its weight should scale with how much judgment the work requires.
