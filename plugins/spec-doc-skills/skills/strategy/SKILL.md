---
description: Design or maintain STRATEGY.md — the product's target problem, approach, users, key metrics, and tracks of work. Use when the user asks to "write our strategy", "set up the strategy doc", "update the roadmap", or names a strategy section to revisit.
argument-hint: "[optional: section to revisit, e.g. 'metrics' or 'approach']"
---

# Strategy Designer

Interview the user with sharp questions, push back on weak answers, and write or maintain `STRATEGY.md` — a short, durable anchor for what the product is, who it serves, how it succeeds, and where the team is investing. It is a strategy doc, not a plan: no features, schedules, or metric values; readable in under five minutes. The input is an optional section name to revisit, plus the existing `STRATEGY.md` if present.

## Process

### 1. Read what's already there

Read `STRATEGY.md`. What's on disk and the argument shape the run:

- No file → interview all five required sections, then write.
- The argument names a section → re-interview just that section, leave the rest untouched.
- A file but no argument → summarize what's on file in a few lines, ask which section to revisit, then interview that one.

Hold a revisited section to the same bar as a first draft.

### 2. Interview

Ask one question at a time with the blocking question tool (numbered options in chat if none exists). Interview the sections in order: target problem, our approach, who it's for, key metrics, tracks. The optional three — milestones, not working on, marketing — are skipped by default; don't push the user to invent them.

Judge every answer against the section standards below. When an answer matches a failure mode, push back with the paired sharper question.

Rules for the back-and-forth:

- **Push back once, maybe twice — then move on.** Name the specific issue and ask a sharper question. If the second answer is still weak, capture what you have, note the section as worth revisiting, and move on.
- **Quote the user back at them.** Challenge with their exact words; a paraphrase softens the challenge and is easy to dismiss.
- **Keep answers to 1–3 sentences.** Long answers usually hide something vague. If you get a paragraph, ask which sentence matters most.
- **Don't reach for the jargon label.** The user doesn't need to hear "that's a vanity metric" — just ask the sharper question.
- **Capture the user's own language.** Don't launder it into generic PM-speak.
- **Ask substantive sections as open questions** inviting free text. Reserve preset options for genuine choices, like which section to revisit — don't hand the user a menu for their own problem statement.

Done when every in-scope required section has an answer that clears its bar, or has been pushed on twice and noted as worth revisiting.

### 3. Write the doc

Fill [assets/strategy-template.md](assets/strategy-template.md) from the captured answers, in the user's own words. Sanity-check the two things most likely to be wrong:

- The target problem and the approach answer each other — the approach is tractable *because of* the specific problem named. If there's no line between them, one of the two is wrong.
- No `{{tokens}}` remain, and `name` plus the H1 title both carry the real product name.

Show the full draft in chat and offer one round of edits. Then write `STRATEGY.md` per the plugin data location config below, with `last_updated` set to today.

Close by offering the natural next step: capturing the jobs the product is hired for and the scenarios it serves with `jtbd`, which builds on the strategy as part of its grounding.

## Plugin Data Location Config

Unless specified otherwise, use the plugin data for where to find and save relevant plugin artifacts.
- **Plugin Data Path** — `${user_config.save_path}`, or `.spec-docs/docs` if `save_path` isn't set. Create it if needed.
- **Save File Name** — `<plugin-data-path>/STRATEGY.md`.
- **File name** — always `STRATEGY.md`.

If the user names a path, use it.

## Section standards

The bar each section must clear before its answer is recorded. Behind all of them, one model: a strategy is a falsifiable choice — a diagnosis (the target problem), a commitment that answers it (the approach), and tracks that carry it out, all pulling the same way. It commits to something competitors could choose *not* to do, which means it also implies what the product is not doing.

### Target problem

*"What's the core problem this product solves — and what makes that problem hard?"*

A strong answer names a specific user situation, says what makes it hard *right now* (a real constraint, not easily routed around), and is falsifiable. Push back on:

- A goal, not a problem ("we need to grow revenue") → "What in the world is making that hard? Whose situation are you changing?"
- A vague wish ("people need better tools for X") → "Whose situation? Doing what? What do they try today, and why doesn't it work?"
- A symptom, not a cause ("users churn after 30 days") → "That's a symptom. What's happening in their world that makes them stop caring?"
- Too broad ("communication at work is broken") → "Narrow it to a situation you can actually affect — which users, doing what, when does it hurt most?"
- A missing feature ("there's no good way to do X with AI") → "What outcome do users want that the feature would give them?"

Capture one or two sentences naming the situation and the crux. No solution language.

### Our approach

*"Given that problem, what's your approach — the commitment that makes it tractable?"*

A strong answer is the guiding choice: how the product wins, such that many downstream decisions get easier, implying alternatives not pursued. Push back on:

- Fluff or values ("we're customer-obsessed and move fast") → "What are you doing *differently* from what users could pick instead? If it applies to any company, it's not your approach."
- A feature list ("AI-powered X, Y, and Z") → "What's the underlying bet that makes you pick those over others?"
- A product description ("we use AI to draft replies") → "Every competitor will say that. What's the *choice* inside it — a grounding bet, a trust commitment, a workflow bet they're not making?"
- The goal restated ("be the market leader") → "How does the product win? What choice are competitors not making?"
- Several approaches at once → "Pick the one that organizes the rest. Which is it?"
- Disconnected from the problem → "How does that approach solve the problem you named? If there's no line between them, one of the two is wrong."

Capture one or two sentences that tie back to the problem ("…so that [outcome]").

### Who it's for

*"Who is the primary user, and what job are they hiring this product to do?"*

A strong answer uses jobs-to-be-done framing — someone in a situation trying to make progress, not a demographic — and names one primary persona. Push back on:

- Too many personas ("founders, PMs, engineers, designers") → "If it's for everyone, it's for no one. Who drives the product decisions?"
- A demographic ("25–45 professionals") → "What are they trying to do that makes them pick this up?"
- A role with no situation ("PMs") → "PMs doing what? Running a review? Writing a spec at midnight? The situation is where the product matters."
- A generic job ("be more productive") → "Productive at what? They're hiring this to do *what*, specifically?"

Capture a persona plus a job sentence, e.g. "Solo founders running their own roadmap. They're hiring the product to keep strategy and execution aligned without a PM on staff."

### Key metrics

*"What 3–5 metrics will tell you whether the approach is working?"*

A strong set mixes leading (moves weekly) and lagging (moves quarterly) and could plausibly regress if the product got worse. Push back on:

- A vanity metric ("total signups, pageviews") → "Those go up while the product gets worse. What moves when users actually get value?"
- Too many ("here are 12") → "A dashboard isn't a strategy. Which 3–5 would you stake the quarter on?"
- An output, not an outcome ("deploys per week") → "That measures the team, not the product. If velocity doubled but users didn't care, is that a win?"
- Something that can only go up ("cumulative hours saved") → "What's the rate or ratio — the thing that can regress?"
- Unmeasurable ("user delight") → "How would you check it on a Tuesday? If you can't, it's aspirational."

Capture 3–5 metrics, each with a one-line definition and where it's measured. If a metric lives nowhere yet, ask whether it can start being measured.

### Tracks

*"What are the 2–4 tracks of work you're investing in to execute the approach?"*

A strong answer names domains of investment broad enough that several features live inside each. Push back on:

- A feature list ("Slack integration; mobile app; dark mode") → "Those are features. What investment area does each live inside? 'Integrations' might be one track."
- Too many ("7 tracks") → "Every track is starved. Which 3 are load-bearing? The rest fold in or drop."
- Disconnected from the approach → "How does that track serve the approach? If it's a separate bet, name it as one."
- Too vague ("improve the product") → "What's the specific investment area that's different from the others?"
- Only one track → "With one track there's no real choice. What are the 2–3 things the product must be good at?"

Capture 2–4 tracks, each with a name, a one-line purpose, and why it serves the approach.

### Optional sections

- **Milestones** — only externally visible ones: a launch, fundraise, conference, renewal. Capture verbatim with dates if named.
- **Not working on** — things the team keeps being tempted by but has decided against. A clarity tool, not a blocker list. One sentence each.
- **Marketing** — a one-liner, tagline, or key message, if the user wants the doc to carry one. Keep to 2–3 lines.
