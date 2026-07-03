---
description: This skill should be used to add a plugin from this marketplace to a repository at project scope so everyone working in the repo gets it (committed to .claude/settings.json). Trigger on requests like "add {plugin} to this project for the team", "enable {plugin} for the repo", or "commit {plugin} to {repo}". Edits and commits one file. Explicit invocation only.
---

# Install a plugin from this marketplace for the project

## Goal

Add a plugin from **this marketplace** at **project scope** so it loads for everyone working in the repository. This commits both the marketplace source and the enable flag to `.claude/settings.json`. The full procedure lives in the guide. Read the guide and run it, keeping it as the single source of truth.

**Guide:** [install-project-scope.md](./install-project-scope.md)

## Confirm before running

Confirm:

- **Which plugin** to add. It comes from this repo's marketplace — read the marketplace name from `.claude-plugin/marketplace.json` (`name` field); the id is `plugin-name@marketplace-name`.
- **Which repository** receives it (the working directory holds the committed `.claude/settings.json`). Most often that is this marketplace repo itself.

Resolve the plugin against this repo's catalog without asking. Ask only when blocked.

## Process

### 1. Read the guide

Read `install-project-scope.md` (in this skill folder) in full for the exact file shape and commands. Treat it as the source of truth; the steps below only frame how to run it.

### 2. Resolve the plugin and catalog it, then gate

The plugin comes from this repo's marketplace. Resolve the request to one plugin folder and make sure it is catalogued:

- Match the request to a single folder under `plugins/`. If the name matches more than one, ask which one. If no folder exists, stop and say it needs creating first (the add-new-plugin skill).
- Check `.claude-plugin/marketplace.json`. If the plugin's folder exists but has no catalog entry, add one — this is what makes it installable. It is a plain local edit to this repo.
- Confirm the working directory is the intended repository.

Ask only when blocked.

### 3. Preview the outcome in one sentence

State plainly what will happen — for example: "This commits `{plugin}` to `{repo}` so everyone working in it gets the plugin."

### 4. Run the guide, and confirm before committing

Follow the guide: catalog the plugin if needed, merge the `extraKnownMarketplaces` and `enabledPlugins` blocks into the committed `.claude/settings.json`, then verify.

**Before committing**, show the change and confirm. The commit is what makes the plugin part of the repo — get explicit approval before making it. Whether and when to push is the user's normal git workflow; this skill does not handle it.

### 5. Recap

Report briefly:

- What was added (`plugin-name@marketplace-name`) at project scope, and that it is committed so it loads for everyone working in the repo.
- **Env to set (if any):** list each key seeded with a placeholder in your gitignored `settings.local.json`, and note that the secret is never committed — so each person must set their own the same way. Omit this line when the plugin needs no user-supplied env.
- **To activate:** the plugin loads after the folder is trusted and a restart or `/reload-plugins`. This step is interactive and remains for each user.
