---
description: This skill should be used to update a plugin maintained in this marketplace repository to a new version and refresh the local install so it picks up the change — bump its version, validate, and refresh the local plugin cache. Trigger on requests like "update {plugin}", "bump {plugin}", "release a new version of {plugin}", or "refresh {plugin} after editing it". Local only — does not commit or push. Explicit invocation only.
---

# Update a plugin and refresh the local install

## Goal

Bump a plugin's version and refresh this machine's install so it picks up the change. The version bump is what makes the refresh real — without it, the install cache keeps the old copy. The full procedure lives in the guide. Read the guide and run it, keeping it as the single source of truth.

This is local only. Committing and pushing the repo — so other machines or remote consumers get the change — is separate and not part of this skill.

**Guide:** [plugin-update.md](./plugin-update.md)

## Confirm before running

Confirm:

- **Which plugin** to update (one in this repo's catalog with a local source).
- The **bump level** — patch (fix), minor (additive), or major (breaking). Infer it from the change when clear; default to patch; ask when unsure.
- That the **change is finished and tested**.

## Process

### 1. Read the guide

Read `plugin-update.md` (in this skill folder) in full for the exact commands. Treat it as the source of truth; the steps below only frame how to run it.

### 2. Confirm the plugin and bump level

- Confirm the named plugin exists in the catalog and has a local source. The `bump` script works only on local-source plugins.
- Pick the bump level from the nature of the change. Ask only when the level is genuinely unclear.

### 3. Preview the plan in one sentence

State plainly what will happen — for example: "This bumps `{plugin}` from `{old}` to `{new}` and refreshes the local install."

### 4. Run the guide

Follow the guide: bump the version, validate with `npm run validate`, then refresh the local install with `claude plugin marketplace update {marketplace}` and `claude plugin update {plugin}@{marketplace}`.

### 5. Recap

Report briefly:

- What changed (`{plugin}` `{old}` → `{new}`) and that the local install was refreshed.
- That a **restart or `/reload-plugins`** is needed to load the new version in the running session.
