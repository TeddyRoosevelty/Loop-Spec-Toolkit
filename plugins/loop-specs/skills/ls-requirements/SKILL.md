---
description: Design a requirements doc from a raw idea — explore genuinely different interpretations, refine to a chosen direction, and capture the decisions. Use when the user brings an idea and wants it explored or opened into options — "explore this idea", "what are different ways to do this".
argument-hint: "[the idea to interpret]"
---

# Requirements Designer

Turn one idea into three genuinely different, grounded ways to build it, then settle on one — with the user by default, or directly when asked. The input is one idea: named in the prompt, or a path to an idea or ideation doc.

## Process

Compress a step when the idea is small enough that it doesn't earn the full treatment — acknowledge the skip rather than silently dropping it.

### 1. Recap, then confirm

Recap the idea back — problem, proposal, constraints, known downsides — in plain language. Confirm you've understood it correctly before running the panel.

### 2. Analyze

Evaluate the idea through multiple perspective exercises to consider the problem from multiple angles. Interpret the results.

#### Run the panel

Spawn the `judgement-analysis` agent once for each exercise in the roster below — all in parallel, in one turn. Each call should:

- **Ask for one exercise**, named exactly as it appears in the roster.
- **Include the same clean writeup of the idea** — that writeup is all the agent has to go on.

A call reads like: *"Run the First Principles exercise on the idea below, then give your report. \<idea writeup\>"*

Don't lead them — no hint at the answer you want or expect; that hands you back your own bias five times.

#### Analyze across the panel

Read across the responses — where they align, where they diverge, and where they question the idea's assumptions or constraints.

### 3. Propose

Turn what the panel surfaced into three real options.

#### Produce the interpretations

Write three interpretations that are *substantively* different — each resting on a different assumption questioned or constraint changed, not three sizes of one idea. Each may rewrite the idea's assumptions, constraints, or scope, as long as it stays grounded in what the panel surfaced. Write each as a standalone, jargon-free idea the reader can follow without the panel output in front of them:

- **Goal** — what this version is really trying to achieve.
- **Proposal** — what you'd actually build, in plain terms.
- **Scope** — what's in, and what's deliberately left out.
- **What it prioritizes** — what this version trades for what.

Close with a plain explanation of what is fundamentally different between the three, and what each one implies.

#### Validate

Check firsthand any fact the interpretations hinge on. Agents may assert things from memory or secondary sources that turn out half-true. Do this before the options go out, so neither the comparison nor the recommendation rests on a wrong fact.

### 4. Present

Present the options for a reader who hasn't seen the panel — the comparison first, then your honest read of where they stand.

#### The options

- **Contextualize.** Lay out the whole picture plainly — what we're focused on and why, giving the background for the ideas, the questions, and where your focus has been for this task.
- **Compare the three.** Side by side in a markdown feature-comparison table — compared attributes with honest tradeoffs (or pros and cons), in an easy-to-understand way.

This is the fair, neutral comparison: the options stand on their own here, before any call is made, and they stay open to challenge in what follows.

#### Honest account

Give an honest read of the three: where each is strong, where it rests on assumptions, and what's known versus still unknown. This is your assessment of where the options stand — not yet a recommendation; the call comes in facilitation.

### 5. Facilitate

Consider what the core questions and concepts are to decide between, based on your analysis and the panel so far. Help the user understand the key inflection points, the problems, the implications, and what they want.

- Use the three options as a facilitation mechanism — a concrete thing to push against — but the depth is in the panel.
- Draw your questions from what the exercises surfaced: the assumptions they questioned, the premise cracks, the cheaper alternative, the real problem underneath.

Facilitate by asking thoughtful questions to uncover insights like:

- Whether these are even the right framings.
- Whether one fits their intent better than it first looked.
- Whether two should merge, or whether the panel points to a stronger direction none of them captured.

Be a thinking partner with small batches of questions at a time, considering what they lean toward before offering your own read. With real options on the table, putting a few concrete choices in front of them to react to is fair — in conversation, not the blocking tool.

The final direction can be one of the three options, a reshaped version, or something new the conversation reached.

Before capturing, reflect the settled direction back: what you're building in a sentence or two, the key trade-offs chosen, what's deliberately out, and anything you'd flag. Keep it short. If the user revises, fold it in and re-confirm rather than writing straight away.

### 6. Capture

Ask what's next with the blocking-question tool — and recommend saving when the direction produced durable decisions worth keeping:

- **Refine in conversation (or stop here)** — no file written; the alignment carries forward in conversation.
- **Save the requirements doc** — write it per [assets/requirements-doc-template.md](assets/requirements-doc-template.md).

## Running autonomously

When asked to just decide or run autonomously, skip facilitation: make the call yourself from the options and say why.

Then run the "Verify on request" step.

## Verify on request

When asked to verify the direction.

Dispatch a new, general adversarial agent to review the draft, briefed to stress-test the requirements; to find where the chosen direction and the trade-offs it rests on don't hold by walking through it.
- Don't bias on the results, tell it what to look for, or guess what it'll find.
- Request it to provide only confirmed, valuable findings over minor or unconfirmed ones. No findings are better than wrong ones.

Review and assess the results provided by the agent. Verify each finding it raises. They could be wrong or misled. Incorporate only what is valid and adds value (even if minor enhancements). Keep at the level of a requirements doc, ignore or adapt any valid feedback if it is outside the purpose of a requirements doc (implementation focused, etc).

## Subagents — the panel
The subagent panel will consist of calling the `loop-specs:judgement-analysis` once per exercise (in parallel):
- First Principles
- Compared-to-what?
- Abstraction Laddering
- Pre-mortem
- Smallest Honest Form

Call that subagent, asking for one of these exercises by name. The agent knows the exercise and how to do it.
- **Do**: Name the exercise to perform and provide the materials for review. 
- **Don't**: don't explain the exercise's steps, bias them with what they should look for, or hypothesize on what they would expect to find.

## Plugin Data Location Config

Unless specified otherwise, use the plugin data for where to find and save relevant plugin artifacts.
- **Plugin Data Path** — `${user_config.save_path}`, or `.loop-specs` if `save_path` isn't set. Create it if needed.
- **Feature folder** — `<plugin-data-path>/<feature-slug>`.
- **Feature slug** — 2–4 words, hyphenated. Before saving, check the existing folders under the plugin data path for any that clearly match (name and recency). Assume a new slug if none clearly match.
- **Save File Name** — `<feature-folder>/requirements.md`. Fixed, lowercase.

Unsure where it should go? Ask with the blocking-question tool (unless running autonomously). Otherwise assume the defaults and confirm the resolved path in the close.

## Writing style

- Write everything — interpretations, the comparison, the recommendation, any questions — to prioritize the reader's understanding.
- Don't narrate the discovery and analysis process. The panel and your analysis are *your* research; use them to shape the options, not as a frame for the conversation.
- Use clear, plain language. Precise language is often needed, but avoid deep jargon and walk through anything that wasn't already clear in the chat.
- Explain what isn't obvious. The reader is not viewing the code, the agent responses, or the docs — and sometimes doesn't have the idea in front of them either.
- Keep questions for the user in their own section — don't bury them in the prose.
- Reserve the blocking-question tool for mechanical decisions with clear answers; judgment, product, and alignment questions belong in conversation, where the context can travel with them.


## Argument Flags
If the user arguments includes any of the following flags, follow them as if they are additional instructions:
--save, --autoSave: Once finalized, save the document in the save set without prompting
--autonomous, --auto: Run in autonomous mode. (see: "Running autonomously")
--verify: Run the "Verify on request" step.
