---
date: 2026-07-03
topic: loop-spec-unified-skill
status: draft
---

# Tech Spec: loop-spec — unified single-skill plugin for building any spec doc

## Summary

A new standalone marketplace plugin, `loop-spec`, containing one skill (`spec`, invoked as `/loop-spec:spec`) that produces any of the 16 spec doc types through a single generalized process. The per-doc substance lives in **spec cards** loaded on demand; **templates are copied verbatim** from `loop-specs`; the process is generalized prose that defers to whichever card is active. This spec settles how those pieces fit and compose — the plugin/asset layout, what a card carries, how the process references it, and how the multi-doc flow runs — grounded in how `loop-specs` skills and this marketplace already work. It does not design the card contents themselves (that is authoring work); it designs the structure they live in.

## Goals & non-goals

**Goals**
- One self-contained skill that builds any of the 16 doc types, matching the quality of the per-doc `loop-specs` skills.
- A reusable **spec card** per doc type, carrying that doc's analysis method and — where it earns it — its quality standards.
- Multi-doc production: align on the doc list and order up front, then produce one doc at a time to completion.
- Zero dependency on `loop-specs`; passes `claude plugin validate ./plugins/loop-spec --strict` and `npm run validate`.

**Non-goals**
- Reproducing the divergent behaviors of the source skills (requirements' 5-agent analysis panel, threat-model's adversary pass). Explicitly dropped.
- Branching or conditional logic written into the process prose.
- Rewriting or re-deriving templates — they are copied as-is.
- Any runtime linkage to `loop-specs` assets.
- Imposing a fixed schema on the cards.

## Proposed design

### Plugin shape

Follows the marketplace's standard layout (per the `add-new-plugin` guide — manifest in `.claude-plugin/`, everything else at the plugin root, self-contained, asset references relative or via `${CLAUDE_PLUGIN_ROOT}`):

```
plugins/loop-spec/
  .claude-plugin/plugin.json      # name "loop-spec", version, author, userConfig.save_path
  skills/spec/
    SKILL.md                       # the generalized process + inline doc catalog
    assets/
      templates/<doc>.md           # 16 files, copied verbatim from loop-specs
      cards/<doc>.md               # 16 files, harvested from each loop-specs skill
```

### The doc catalog

A table **inline in SKILL.md** — one row per doc type with a one-line "use when", plus that doc's card path, template path, and output filename. Selecting the doc(s) is the skill's first job, so this small always-loaded table (16 short lines) belongs in the body; the heavier per-doc cards stay in progressive disclosure and load only when a doc is chosen.

### Spec cards

One card per doc type at `assets/cards/<doc>.md`, harvested from the matching `loop-specs` skill. A card is **not forced into a fixed template** — each is authored in whatever shape gives good results for its doc. What every card must make available to the process:

- **Analysis method** — what to read and gather for this doc (e.g. extract-from-code, harvest-terms), including whether to scale to parallel search agents on a large surface. This is what the generic process defers to.
- **Template pointer** — relative link to `../templates/<doc>.md`.
- **Output filename** — the fixed save name (e.g. `architecture.md`).
- **Standards — where they earn their place.** The concrete quality bar, included only where it adds real signal beyond what the template already communicates, authored lean and specific to the doc. (See Risks: carrying standards is riskier than omitting them.)

The card carries the doc-specific substance so the process can stay generic. Its shape adapts to the doc; only its job is fixed, not its format.

### The generalized process (in SKILL.md)

One prose flow adapted from the shared six-step skeleton the `loop-specs` skills follow. It never branches on doc type — it defers to the active card.

1. **Select & sequence** — from the task, decide which doc(s) are needed and in what order, using the catalog; align that list and order with the user before producing anything.
2. **For each doc in order, run the full process to completion, then move to the next:**
   - **Ground** — read the active doc's card and template, and any prior source doc.
   - **Analyze** — per the card's analysis method; scale to the surface (read directly, or dispatch parallel search agents for a large one).
   - **Draft** — fill the template.
   - **Present** — the draft plus an honest account, held against the card's standards where present.
   - **Facilitate** — refine with the user.
   - **Capture** — save to the card's output filename in the feature folder.

The generalization is by *deferral to data* (the card), not by conditionals in the prose — the anti-theatre principle that also governs the cards.

### Supporting sections

Generalized from the source skills, which carry these near-identically already:
- **Autonomous mode** — skip facilitation; run verify instead.
- **Verify on request** — dispatch an adversarial agent to stress-test the draft against the active card's standards.
- **Save-location config** — its own copy of the `save_path` userConfig pattern (`.loop-specs` default), feature-slug folder, per-doc output filename from the card.
- **Writing style** and **argument flags** (`--save`, `--auto`, `--verify`).

## Alternatives considered

- **Combined "spec pack" (card + template in one file per doc)** instead of separate `cards/` and `templates/`. Would win if we wanted one link per doc and didn't value template purity. Rejected: separate files keep the copied template pristine and verifiable against `loop-specs`, and give finer progressive disclosure — load the small card first, the template only at draft time.
- **Separate index file for the catalog** instead of inline in SKILL.md. Would win if SKILL.md grew uncomfortably large. Rejected: 16 one-liners is small, selection needs them on the first turn, and an extra read to decide which docs is friction.
- **Externalize the process to a linked file.** Would win if the process grew long enough to bloat SKILL.md. Rejected: the process is the cornerstone and always needed — keeping it in the body is where a well-written skill lives.
- **Fixed card schema (identical headers across all 16).** Would win for authoring consistency. Rejected: a rigid template on the cards is the same procedural theatre we're avoiding in the process; cards adapt to their doc.
- **Pure menu selection** (ask the user to pick from 16). Rejected: the skill infers the doc list and order, then confirms — inference-then-align, not a menu.

## Risks & open questions

**Blocks building — decided:**
- **Plugin name / namespace.** Settled: plugin `loop-spec`, skill `spec` → `/loop-spec:spec`.

**Settle-able in implementation (won't force rework):**
- **Authoring the cards is the real work, and the standards are the delicate part.** The template already defines what belongs in the doc. The card's standards are a supplement, and carrying them is *riskier than omitting them*: criteria that are disconnected from the specific doc, or that over-instruct, bias the model and muddy what we're actually asking for. The failure mode is not "it builds a bad document" — it's "we author the wrong thing into the card, or stop communicating clearly what we want." Mitigation: include standards only where they add real signal beyond the template, authored lean and doc-specific, never as boilerplate. This is authoring discipline, not a design change.
- **Generative doc types are lighter here by design.** The requirements and JTBD cards describe a simpler analysis method without their source skills' special machinery (the panel, etc.). Consistent with "divergences not precious," but named so it's a known, intended simplification rather than a surprise.
- **Template drift.** Templates are copied verbatim with no sync back to `loop-specs`; if the source templates change later, these won't. Accepted cost of the clean boundary.
- **Marketplace registration mechanics.** The `add-new-plugin` guide notes installation is what lists a plugin in `marketplace.json` (though `loop-specs` is listed manually). A build-step detail, not a design concern.
```

Note: this spec designs the structure the cards live in; the card *contents* — the harvested analysis methods and standards — are the quality-critical authoring work, done during the build.
