---
description: Survey a subject — a whole repo or a single focus — for its strongest problems and opportunity gaps, and return a shortlist of candidate ideas worth developing. Use when the user wants options to choose from — "find ideas to improve X," "what's worth doing here" — rather than bringing one idea of their own to develop.
argument-hint: "[the subject or focus to explore]"
---

# Ideation

Survey a subject, find the problems and opportunity gaps worth acting on, and return a shortlist of candidate ideas. Your job is to find and frame the candidates — not to develop them into options, plans, or code. The input is a subject or focus, anywhere from a whole repo to a single feature, sometimes with supporting material.

## Process

Match the depth to the subject. 

### 1. Ground in the subject

Read the `STRATEGY.md`, `JTBD.md`, and any materials provided — the direction the project's gaps are measured against.

### 2. Analyze

Analyze the project against the strategy and goals to find where it falls short.

- **Find the gaps.** Identify discrepancies, misalignments, problems, and opportunity gaps against the direction and materials.
- **Trace to the areas that move them.** The principle areas that would need to change to improve alignment or meet the goal.
- **Merge what's coupled.** Treat issues with a shared root cause or a coupled solution as a single issue.

Match the count to the subject: a narrow focus may surface one improvement opportunity or none; a broad one, up to seven of the most impactful.

### 3. Propose

Develop your ideas.

#### Produce the proposals

For each distinct problem, propose a feature-level solution — how to resolve that tension, gap, or problem. Keep it high level but targeted at the specific problem it answers.

#### Validate

Run a validation check on the candidates. Dispatch a `spec-doc-skills:judgement-analysis` agent:

* Ask it to run the First Principles, Compared-to-what?, and 5-Whys exercises and review each idea
* Provide the problems and the idea proposed for each

Don't explain the exercises' steps, tell it what to look for, or guess what it'll find.

Review feedback and incorporate. Verify or resolve any open questions and confirm the load-bearing claims now, so the candidates do not rests on a wrong assumptions or framings.

### 4. Present

Present the candidates clearly and concisely. Balance understanding and brevity, and write so the reader can follow without the code, your investigation, or the docs in front of them.

#### The candidates

- **Open with context.** A brief introduction to the ideas and the angles they approach from.
- **Then the ideas.** Each with brief context for what it is: the goal, how it helps a problem or gap, and a short justification.

Keep the ideas and their context as the focus. Don't present the problems as a standalone set or a one-to-one mapping with the solutions — mention them in the context or idea details where it fits, explained plainly for a reader seeing them for the first time.

#### Honest account

List the healthy areas and the flagged issues, so the user sees what you ruled out, not just what you kept. Then give an honest read of the candidates: if any are strong, where the set or items rests on assumptions, and what's known versus still unknown.

### 5. Facilitate

Surface the **load-bearing questions** — the core questions whose answers would most sharpen or re-aim the candidate set: the real trade-offs the investigation exposed, and what's still unknown about intent or context. These are questions of judgment and direction — strategic or tactical — that could re-ground the candidates, not implementation details of the proposed solutions.

- Use the candidates as a facilitation mechanism — a concrete thing to push against — but set the depth from the problem/opportunity gap analysis.
- Keep the questions few and high-leverage. Raise them in conversation in their own section, not through the blocking-question tool.

As the questions get answered, fold the answers into your analysis and candidate set. The result can re-affirm your ideas, reshape them, or signal a need to rethink the set fresh; when something fundamental shifts, rework the shortlist and present it as a new version, routing deeper reworks back to the step that owns them.

When facilitation changes the ideas, re-present them — pick the form that fits how much moved:

- **Recap** — a short summary of what changed, when the changes are small.
- **Full set** — relist the full updated set, when much of it moved.
- **As-is** — acknowledge you'll use the ideas as presented, when nothing changed.

Don't mix commentary with the re-presentation, and when an idea changed, produce its full writeup again.

### 6. Capture

Saving is opt-in. Ask what's next with the blocking-question tool:

- **Refine in conversation (or stop here)** — add candidates, re-investigate, or go deeper on one. No file written.
- **Save** — write the record per [assets/ideation-record-template.md](assets/ideation-record-template.md).

Before saving, make any final refinements that help the candidates read clearly.

## Running autonomously

When asked to run autonomously, skip facilitation. Before saving, default to running the defined verification-step (below).

## Verify on request

When asked to verify the shortlist, run a self-assessment of the ideas provided. Consider each idea through a set of
- **First Principles Exercise** — strip the idea down to facts you can verify, separate those facts from the assumptions riding on top of them, and check whether the idea still holds when it rests only on what is proven. Surfaces misleading or oversold framing.
- **Compared-to-what Exercise** — weigh the idea against its real alternatives, most importantly the do-nothing baseline (what happens if we simply don't do this), but also the cheaper, simpler, or already-available options it is competing with. Tests whether it is worth doing at all.
- **5-Whys Exercise** — starting from the idea as stated, ask "why" repeatedly to trace past the surface motivation down to the root problem it is actually trying to solve, and check whether the idea is the right response to that root.

Research and check any claims you are not sure about.

Then, weigh which of your own critiques actually adds value, fold those in, and re-present what changed.

## Plugin Data Location Config

Unless specified otherwise, use the plugin data for where to find and save relevant plugin artifacts.
- **Plugin Data Path** — `${user_config.save_path}`, or `.spec-docs/docs` if `save_path` isn't set. Create it if needed.
- **STRATEGY.md** — `<plugin-data-path>/STRATEGY.md`
- **JTBD.md** — `<plugin-data-path>/JTBD.md`
- **Ideation folder** — `<plugin-data-path>/ideation`.
- **Save File Name** — `<ideation-folder>/YYYY-MM-DD-<topic>-ideation.md`
- **File name** — today's date and the topic; use `-open-ideation.md` when there's no topic or focus.

Unsure where it should go? Ask with the blocking-question tool. Otherwise assume the defaults.

Read `STRATEGY.md` and `JTBD.md` directly with the Read tool, using the location provided. If a file isn't at that location, or its location isn't defined in context, skip it immediately. Do not search.

## Candidate standards

The bar a candidate clears before it earns a spot on the shortlist. A strong candidate is:

- **Grounded** — it traces to something specific you saw: a file, a flow, a behavior, a pattern. A gap clears a higher bar than a problem, because it needs a real present driver, not a guess about the future.
- **At the right level** — the root, not a symptom; not a cosmetic nit, not a vague theme.
- **Significant** — it earns team discussion. You can say plainly who it hurts or what value goes unused. It sits at the feature level, not a typo or a one-off bug.
- **Distinct** — it stands apart from the others, not a reword of another candidate.
- **In bounds** — you can sharpen, widen, or reframe the subject as the evidence pushes you to, but don't wander into a different project. The named focus is the constraint. Material you scanned and research you did are background: they can back a candidate, but they must not drag the set toward whatever shouted loudest in them.

## Writing style
- Write everything — interpretations, comparisons, recommendations, any questions — to prioritize the reader's understanding.
- Don't narrate the discovery and analysis process. Instead, present the findings for interpretation.
- Use clear, plain language. Precise language is often needed, but avoid deep jargon and walk through anything that wasn't already clear in the chat.
- Explain what isn't obvious. The reader is not viewing the code, resources, your investigation, or the docs — and sometimes doesn't have the idea in front of them either.
- Keep questions for the user in their own section — don't bury them in the prose.
- Reserve the blocking-question tool for mechanical decisions with clear answers; judgment, product, and alignment questions belong in conversation, where the context can travel with them.
