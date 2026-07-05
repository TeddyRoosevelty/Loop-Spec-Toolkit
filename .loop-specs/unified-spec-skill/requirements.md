# Unified Spec Skill — one-stop plugin for building any spec doc

## Problem Statement

The `loop-specs` plugin ships ~16 separate skills, one per spec doc type (requirements, architecture, data model, API contract, threat model, test strategy, task brief, work breakdown, conventions, glossary, NFRs, risk register, JTBD, assumptions, QA plan, tech spec). That granularity gives users fine control, but it's a large footprint and forces the user to know which of many skills to reach for. Not everyone wants that control. There's no single place to go to get a spec doc produced.

## Objectives

- Give users a **one-stop shop**: a single skill that can build any of the spec doc types, for a smaller footprint than 16 separate skills.
- Preserve the **quality** of the docs produced — they should be as grounded and non-generic as what the individual skills produce today.
- Stand **fully on its own** — a separate plugin that doesn't cross into or depend on `loop-specs`.

## Who it's for

Users who want a single, low-footprint entry point for producing spec docs and don't need the fine-grained control of invoking a dedicated skill per doc type. It's an alternative to the per-doc skills, not a replacement for them.

## In Scope

- A **new, standalone plugin** in this marketplace containing exactly **one skill**.
- Building **any** of the ~16 spec doc types that `loop-specs` covers.
- A **generalized process** — one "steps to follow for creating a spec" flow, adapted from the shared six-step skeleton the existing skills follow (ground → analyze → draft → present → facilitate → capture).
- **Spec cards** — one per doc type, carrying that doc's analysis method and quality standards, loaded via progressive disclosure for the doc currently being built. Harvested from the existing skills' standards and analysis prose.
- **Templates** — copied as-is (verbatim) from `loop-specs` into the new plugin's own assets.
- **Multi-doc, sequential production** — given a task, the skill first decides and aligns with the user on the list of docs and their order, then produces them one at a time, running the full process to completion for each before starting the next.

## Out of Scope

- Any reference to, dependency on, or shared code/assets with `loop-specs` — the plugin is self-contained.
- Re-deriving or rewriting the templates — they are copied as-is.
- Reproducing the divergent, doc-specific behaviors of the current skills (e.g. the requirements 5-agent analysis panel, the threat-model adversary pass). The generalized process is the point; these are deliberately not carried over.
- Retiring or modifying the existing per-doc `loop-specs` skills — they stay as they are, independent of this plugin.
- Procedural branching written into the process prose (`if doc == X then …`). The process is well-written prose a capable model follows and adapts; per-doc specifics come from the loaded spec card, not from conditionals in the process.
- Producing multiple docs in parallel — production is strictly one at a time.

## Requirements

**Structure**

- The plugin is standalone and self-contained; it carries its own copy of every asset it uses.
- It contains a single skill that can produce any supported doc type.
- Its assets are: the copied templates, one spec card per doc type, and the generalized process (in the skill body).

**The generalized process**

- Adapted from the shared six-step skeleton, written as clean prose — not pseudocode or conditional branching.
- The doc-specific substance (what to analyze, the quality bar to clear) is supplied by the spec card loaded for the doc being built, not baked into the process.
- Retains the shared supporting behavior the existing skills carry where it applies generically (e.g. facilitation with the user, save/capture, autonomous mode) — adapted, not per-doc.

**Spec cards**

- One card per doc type, each carrying that doc's analysis method and its concrete quality standards — the same substance that keeps today's docs non-generic, relocated from each skill's prose into a card.
- Loaded via progressive disclosure, only for the doc currently being produced.
- Authored by harvesting from the corresponding existing skill (its standards block and analysis approach), since that material lives in the SKILL.md files rather than in the templates.
- Designed as a first-class, reusable asset — intended to hold up as an intermediary building block regardless of how the skill evolves later.

**Templates**

- Copied verbatim from `loop-specs`; not adapted or rewritten.

**Flow**

- On invocation, the skill first determines which doc(s) the task needs and in what order, and aligns on that list and order with the user before producing anything.
- It then produces each doc in order, running the full generalized process to completion for one doc before moving to the next.

## Acceptance Criteria

- A new plugin exists in the marketplace, separate from `loop-specs`, containing one skill.
- The plugin has no reference to, import from, or runtime dependency on `loop-specs`; it works if `loop-specs` is absent.
- The skill can produce every supported doc type, each grounded and non-generic — matching the quality of the corresponding `loop-specs` skill's output.
- Each supported doc type has a spec card carrying its analysis method and concrete standards, and a copied template.
- Given a task, the skill proposes a doc list and order, confirms it with the user, then produces the docs one at a time to completion.
- The process prose is generalized and free of doc-specific conditional branching; per-doc behavior is driven by the loaded spec card.

## Outstanding Questions

**Can be answered during planning**

- The exact set of doc types to include at launch — assumed to be the full ~16 that `loop-specs` covers.
- How the spec card and copied template are structured relative to each other (one combined asset per doc vs. two separate files).
- Which supporting sections of the existing skills (autonomous mode, verify-on-request, argument flags, save-location config) the generalized skill keeps, and in what generalized form.
- Where the plugin saves its output — whether it reuses a `save_path`-style user config like `loop-specs` or defines its own.
