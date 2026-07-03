---
description: This skill should be used to remove a plugin from a project or machine — figure out where it is enabled (local, project, or user scope) and turn it off there. Trigger on requests like "remove {plugin} from this repo", "uninstall {plugin}", "turn off {plugin} for the team", or "take {plugin} off my machine". The user names the plugin; the skill finds its scope and removes it. Explicit invocation only.
---

# Remove a plugin

## Goal

Turn a plugin off and take it out of the settings that enable it. A plugin can be enabled at three scopes — **local** (one repo, just you), **project** (one repo, everyone working in it), or **user** (every project on your machine) — and each removes differently. The skill's job is to find where the plugin is actually enabled, then run the matching removal from the right place. The full procedure lives in the guide. Read the guide and run it, keeping it as the single source of truth.

**Guide:** [uninstall-plugin.md](./uninstall-plugin.md)

## Confirm before running

Confirm:

- **Which plugin** to remove.
- **Which scope** it is being removed from — read this from `claude plugin list`, don't guess. If the same plugin is enabled at more than one scope, confirm which one (or all) the user means.

Resolve the scope and location without asking where you can. Ask only when blocked or when removal reaches other people (see step 2).

## Process

### 1. Read the guide

Read `uninstall-plugin.md` (in this skill folder) in full for the exact commands per scope. Treat it as the source of truth; the steps below only frame how to run it.

### 2. Resolve the plugin and its scope, then gate

Resolve the request to one exact `plugin-name@marketplace-name` id and the scope it is enabled at:

- Run `claude plugin list` to read the current state. The `Scope` line on each entry tells you where it is enabled.
- Match the request to a single plugin. If the name matches more than one, ask which. If the plugin is not enabled anywhere, report that and stop — there is nothing to remove.
- If it is enabled at more than one scope, list those scopes and confirm which the user wants removed before touching anything.

**Scope decides the gate:**

- **Local** removal is cwd-sensitive. The on-switch lives in that repo's gitignored `.claude/settings.local.json`, so the command must run from that repo's root. Confirm the working directory is that repo before running, or you will no-op (or remove it from the wrong repo).
- **Project** removal edits the committed `.claude/settings.json`, so it stops the plugin loading for everyone working in the repo. Show the change and get explicit approval before committing. Whether and when to push is the user's normal git workflow; this skill does not handle it.
- **User** removal is machine-wide but private to you; no commit, no one else affected.

During resolution, ask only when genuinely blocked — an ambiguous plugin name or more than one scope to choose from. The confirmation that the removal itself is expected happens next, in step 3.

### 3. State what will happen, and confirm

There are three ways to remove a plugin and each lands differently, so before running anything, say plainly which one this is and what it touches — then **wait for the user to confirm** it is what they expect:

- **Local** — "This turns `{plugin}` off for you in `{repo}` only. Nothing is committed and no one else is affected."
- **User** — "This removes `{plugin}` from your machine, so it stops loading in every project. Private to you, nothing committed."
- **Project** — "This removes `{plugin}` for everyone working in `{repo}`, and it is committed."

Confirm before acting because each scope has a different blast radius — a local removal touches only you, a project removal reaches everyone working in the repo. Get explicit approval here; for project scope, this is also the approval to commit.

Note: Answering a separate but related implementation question does not count as confirmation. You must highlight the change separate from any questions.

### 4. Run the guide

Follow the guide for the resolved scope: run the matching uninstall (or edit and commit, for project scope), then verify the entry is gone.

### 5. Recap

Report briefly:

- What was removed (`plugin-name@marketplace-name`) and from which scope, said in functional terms (just you in one repo / everyone working in the repo / your whole machine).
- For project scope: that the change is committed and stops loading for everyone working in the repo on their next reload.
- **To apply now:** restart Claude Code or run `/reload-plugins`. The plugin keeps loading in the current session until then. This step is interactive and remains for the user to do.
