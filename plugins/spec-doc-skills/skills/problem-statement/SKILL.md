---
description: Design a problem statement — the specific problem or opportunity worth solving, grounded in evidence and stated before any solution. Use when the user wants to pin down the problem first — "what problem are we really solving", "write up this problem" — rather than explore ways to build something.
argument-hint: "[the problem or opportunity area to frame]"
---

# Problem Statement Designer

Turn one stated problem into a few genuinely different, evidence-grounded framings of what's really wrong, then settle on one — with the user by default, or directly when asked. The input is one problem or opportunity: named in the prompt, or a pointer to notes, an idea, or an ideation doc. Frame the problem, not a solution.

## Process

Read [assets/problem-statement-template.md](assets/problem-statement-template.md) up front — it's the artifact the chosen framing fills. Compress a step when the problem is small enough that it doesn't earn the full treatment — a sharp problem with one obvious root goes straight to a single framing; acknowledge the skip rather than silently dropping it.

### 1. Recap, then confirm

Read any notes, idea, or materials the user pointed to — the problems that matter to the product and who they hurt.

Recap the problem back — the situation, who it seems to hurt, what the user thinks it costs — in plain language. Treat that recap as the *stated* frame, not the truth: confirm you've got the right starting point before digging in, knowing the real problem may sit above or below it.

When there's no anchoring direction, say so and work from what the user tells you; the framings still ground in real evidence.

### 2. Analyze

Find what's really wrong beneath the stated problem, and the few honest ways it could be framed — grounded in evidence and considered from multiple angles.

If the evidence points to one honest root, say so and draft it directly; run the panel and produce framings when the root is genuinely in doubt or the stakes are high.

#### Ground in the evidence

Read the code, materials, or data the problem touches yourself, first-hand. Find what shows the problem is real and at the scale claimed, and hold what the evidence proves apart from what's assumed on top of it. Treat the stated problem as a candidate symptom and the claimed cost as a claim to test. Scale the method to the surface: read directly for a small area; dispatch parallel search agents for a large or unfamiliar one, then verify the load-bearing findings yourself.

#### Run the panel

Spawn the `judgement-analysis` agent once for each exercise in the roster below — all in parallel, in one turn. Each call should:

- **Ask for one exercise**, named exactly as it appears in the roster.
- **Include the same clean writeup of the problem and its evidence** — that writeup is all the agent has to go on.

A call reads like: *"Run the 5-Whys exercise on the problem below, then give your report. \<problem writeup\>"*

Don't lead them — no hint at the root you suspect or the answer you expect; that hands you back your own anchor several times over.

#### Analyze across the panel

Read across the responses — where they agree on the root, where they place the problem at different altitudes, and where they trace the pain to a different cause or a different party. The distinct framings the evidence can support are the candidates; a framing no evidence backs is a guess, not a candidate.

### 3. Propose

Turn what the panel surfaced into the real candidate framings, then check they hold.

#### Produce the framings

Write the few framings the evidence supports — usually two or three, *substantively* different, each resting on a different root, altitude, or affected party, not three sizes of one problem. Write each as a standalone, jargon-free framing the reader can follow without the panel output in front of them:

- **The problem** — what's really wrong, at this framing's root and altitude.
- **Who it hurts** — the party this framing puts at the center.
- **The evidence** — what shows it's real and at the scale claimed.
- **What solving it changes** — the outcome wanted, stated as an outcome, never the thing to build.

Close with a plain explanation of how the framings relate — which sits deeper than another, which traces to a separate cause — and what each implies. Every framing stays solution-free.

#### Validate

Check firsthand any fact a framing hinges on — the evidence and the claimed scale most of all. Agents may assert things from memory or secondary sources that turn out half-true. Do this before the candidates go out, so neither the comparison nor the recommendation rests on a wrong number. Confirm each framing reads as a problem and an outcome, with no solution smuggled in, and clears the problem standards below.

### 4. Present

Present the framings for a reader who hasn't seen the panel — the comparison first, then your honest read of where they stand.

#### The candidates

- **Contextualize.** Lay out the whole picture plainly — the stated problem, what the evidence showed, and where your focus has been for this task.
- **Compare the framings.** Side by side in a markdown table — each framing's root, who it hurts, the evidence behind it, what solved would look like, and how sure it is. Show how they relate — up or down the ladder, or a separate cause — so the choice is between real, distinct theories of the problem.

This is the fair, neutral comparison: the framings stand on their own here, before any call is made, and they stay open to challenge in what follows.

#### Honest account

Give an honest read of the framings: which the evidence best supports, where each rests on assumptions about cost or intent, and what's known versus still unknown. This is your assessment of where they stand — not yet a recommendation; the call comes in facilitation.

### 5. Facilitate

Consider the core questions to decide between, based on your analysis and the panel so far. Help the user see the framing decisions that matter — the altitude, the root, and who the problem really centers on.

- Use the framings as a facilitation mechanism — a concrete thing to push against — but the depth is in the evidence and the panel.
- Draw your questions from what the exercises surfaced: the symptom-versus-root question, the cheaper read of the same pain, the party the stated frame left out.

Facilitate by asking thoughtful questions to uncover insights like:

- Whether this is the real problem, or one level up or down from it.
- Whether the impact is worth a body of work, against the do-nothing baseline.
- Whether two framings collapse into one, or the panel points to a sharper problem none of them captured.

Be a thinking partner with small batches of questions at a time, considering what they lean toward before offering your own read. With real framings on the table, putting a few concrete choices in front of them to react to is fair — in conversation, not the blocking tool.

The settled problem can be one of the framings, a reshaped version, or a sharper problem the conversation reached.

Before capturing, reflect the settled problem back: what's really wrong in a sentence or two, who it hurts, what solved looks like, and anything you'd flag. Keep it short. If the user revises, fold it in and re-confirm rather than writing straight away.

### 6. Capture

Save only when the user asks or confirms. Ask what's next with the blocking-question tool:

- **Refine in conversation (or stop here)** — no file written; the alignment carries forward in conversation.
- **Save** — write the statement per the template and the plugin data location config below, with `last_updated` set to today.

## Problem standards

The bar every framing clears, and the chosen problem most of all. A strong statement is:

- **Grounded** — it traces to real evidence you saw: data, a behavior, code, a user signal — not an assertion that the problem exists.
- **Root, not symptom** — it names what's actually driving the pain, not the surface complaint.
- **Solution-free** — it states the problem and the outcome wanted, never the thing to build. A problem written as "we lack feature X" is a solution wearing a problem's clothes.
- **Worth solving** — the cost of leaving it is real and statable, and beats the do-nothing baseline.
- **Falsifiable** — what "solved" looks like is concrete enough that you could later tell whether it was.

## Running autonomously

When asked to just decide or run autonomously, skip facilitation: make the call yourself from the framings and say why.

Then run the "Verify on request" step.

## Verify on request

When asked to verify the statement.

Dispatch a new, general adversarial agent to review the draft, briefed to stress-test the problem statement; to find where its root, evidence, and claimed impact don't hold by walking through it.
- Don't bias on the results, tell it what to look for, or guess what it'll find.
- Request it to provide only confirmed, valuable findings over minor or unconfirmed ones. No findings are better than wrong ones.

Review and assess the results provided by the agent. Verify each finding it raises. They could be wrong or misled. Incorporate only what is valid and adds value (even if minor enhancements). Keep at the level of a problem statement — ignore or adapt any valid feedback that pulls toward a solution.

## Subagents — the panel

The framing panel is one `spec-doc-skills:judgement-analysis` call per exercise (in parallel):
- First Principles
- 5-Whys
- Abstraction Laddering
- Compared-to-what?

Call that subagent, asking for one of these exercises by name. The agent knows the exercise and how to do it.
- **Do**: name the exercise to perform and provide the problem writeup and its evidence for review.
- **Don't**: don't explain the exercise's steps, bias them with what they should look for, or hypothesize on what they would expect to find.

## Plugin Data Location Config

Unless specified otherwise, use the plugin data for where to find and save relevant plugin artifacts.
- **Plugin Data Path** — `${user_config.save_path}`, or `.spec-docs` if `save_path` isn't set. Create it if needed.
- **Feature folder** — `<plugin-data-path>/<feature-slug>`.
- **Feature slug** — 2–4 words, hyphenated. Before saving, check the existing folders under the plugin data path for any that clearly match (name and recency). Assume a new slug if none clearly match.
- **Save File Name** — `<feature-folder>/problem-statement.md`. Fixed, lowercase.

Unsure where it should go? Ask with the blocking-question tool (unless running autonomously). Otherwise assume the defaults and confirm the resolved path in the close.

## Writing style

- Write everything — the framings, the comparison, the recommendation, any questions — to prioritize the reader's understanding.
- Don't narrate the grounding and analysis process. The evidence and the panel are *your* research; use them to shape the framings, not as a frame for the conversation.
- Use clear, plain language. Precise language is often needed, but avoid deep jargon and walk through anything that wasn't already clear in the chat.
- Explain what isn't obvious. The reader isn't viewing the code, the agent responses, or the docs — and sometimes doesn't have the problem in front of them either.
- Keep questions for the user in their own section — don't bury them in the prose.
- Reserve the blocking-question tool for mechanical decisions with clear answers; judgment, framing, and direction belong in conversation, where the context can travel with them.
