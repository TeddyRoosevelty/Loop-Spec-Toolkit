---
description: This skill should be used to add a plugin from this marketplace for the current user in one repository only (local scope, gitignored, not shared with teammates). Trigger on requests like "install {plugin} just in this repo", "add {plugin} locally for me", or "use {plugin} in {repo} without committing it". The user names the plugin; the skill catalogs and installs it. Explicit invocation only.
---

# Install a plugin from this marketplace for yourself in one project

## Goal

Install a plugin from **this marketplace** at **local scope** so it loads for the current user in one repository only, without being shared. The full procedure lives in the guide. Read the guide and run it, keeping it as the single source of truth.

**Guide:** [install-local-scope.md](./install-local-scope.md)

## Confirm before running

Confirm two things:

- **Which plugin** to install. It comes from this repo's marketplace — read the marketplace name from `.claude-plugin/marketplace.json` (`name` field); the id is `plugin-name@marketplace-name`.
- **Which repository** receives the on-switch. Local scope writes to the current directory's `.claude/settings.local.json`, so the working directory must be the intended repo.

Resolve the plugin against this repo's catalog without asking. Ask only when blocked (see step 2).

## Process

### 1. Read the guide

Read `install-local-scope.md` (in this skill folder) in full for the exact commands. Treat it as the source of truth; the steps below only frame how to run it.

### 2. Resolve the plugin and catalog it, then gate

The plugin comes from this repo's marketplace. Resolve the request to one plugin folder and make sure it is catalogued:

- Match the request to a single folder under `plugins/`. If the name matches more than one, ask which one. If no folder exists, stop and say it needs creating first (the add-new-plugin skill).
- Check `.claude-plugin/marketplace.json`. If the plugin's folder exists but has no catalog entry, add one — this is what makes it installable. It is a plain local edit to this repo.
- If this repo's marketplace (its `name` in `.claude-plugin/marketplace.json`) is not registered (`claude plugin marketplace list`), add this repo as the source per the guide.
- Confirm the working directory is the intended repo. If a different repo was named, change to it (or ask) before installing. If the plugin is already installed at local scope here, report that and stop.

Ask only when blocked.

### 3. Preview the outcome in one sentence

State plainly what will happen — for example: "This turns `{plugin}` on for the current user in `{repo}` only, and is not shared."

If the request implies sharing with the team, flag the mismatch first: this skill is private and gitignored. Confirm the project (team) skill was not intended before continuing.

### 4. Run the guide

Follow the guide: catalog the plugin if needed, confirm the marketplace is registered, install at local scope from the repo root, then verify the result lands in the gitignored `.claude/settings.local.json`.

### 5. Recap

Report briefly:

- What was installed (`plugin-name@marketplace-name`), at local scope in `{repo}` — private to the current user.
- **Env to set (if any):** list each key seeded with a placeholder and note it needs a real value. These are secrets and stay in the gitignored `settings.local.json` only. Omit this line when nothing was seeded.
- **To activate:** restart Claude Code or run `/reload-plugins`. This step is interactive and remains for the user to do.
