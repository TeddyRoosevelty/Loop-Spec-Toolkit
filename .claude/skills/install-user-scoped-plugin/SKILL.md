---
description: This skill should be used to add a plugin from this marketplace for the current user across all projects on this machine (user scope). Trigger on requests like "install {plugin} for me everywhere", "add {plugin} to all my projects", or "enable {plugin} globally". The user names the plugin; the skill catalogs and installs it. Explicit invocation only.
---

# Install a plugin from this marketplace for yourself across all projects

## Goal

Install a plugin from **this marketplace** at **user scope** so it loads in every project on this machine. The full procedure lives in the guide. Read the guide and run it, keeping it as the single source of truth.

**Guide:** [install-user-scope.md](./install-user-scope.md)

## Confirm before running

Confirm only **which plugin** to install. It comes from this repo's marketplace — read the marketplace name from `.claude-plugin/marketplace.json` (`name` field); the id is `plugin-name@marketplace-name`. Resolve every other input — whether it is catalogued, whether the marketplace is registered — without asking. Ask only when genuinely blocked (see step 2).

## Process

### 1. Read the guide

Read `install-user-scope.md` (in this skill folder) in full for the exact commands. Treat it as the source of truth; the steps below only frame how to run it.

### 2. Resolve the plugin and catalog it, then gate

The plugin comes from this repo's marketplace. Resolve the request to one plugin folder and make sure it is catalogued:

- Match the request to a single folder under `plugins/`. If the name matches more than one, ask which one. If no folder exists, stop and say it needs creating first (the add-new-plugin skill).
- Check `.claude-plugin/marketplace.json`. If the plugin's folder exists but has no catalog entry, add one — this is what makes it installable. It is a plain local edit to this repo.
- If this repo's marketplace (its `name` in `.claude-plugin/marketplace.json`) is not registered (`claude plugin marketplace list`), add this repo as the source per the guide.
- If the plugin is already installed at user scope, report that and stop.

Ask only when blocked. When the plugin resolves and its marketplace is present, proceed without questions.

### 3. Preview the outcome in one sentence

State plainly what will happen, in functional terms — for example: "This turns `{plugin}` on in every project on this machine."

If the request named a specific repo or project, flag the mismatch first: this skill is machine-wide. Confirm the one-project or team skill was not intended before continuing.

### 4. Run the guide

Follow the guide: catalog the plugin if needed, confirm the marketplace is registered, install at user scope, then verify the result.

### 5. Recap

Report briefly:

- What was installed (`plugin-name@marketplace-name`), at user scope — every project on this machine.
- **Env to set (if any):** list each key seeded with a placeholder in `~/.claude/settings.json` and note it needs a real value. These are secrets and stay in that private machine config only. Omit this line when nothing was seeded.
- **To activate:** restart Claude Code or run `/reload-plugins`. This step is interactive and remains for the user to do.
