# Install a plugin from this marketplace for yourself on one project

Turn a plugin from **this marketplace** on for yourself in **one** repository only (local scope). Nothing is shared — the on-switch lives in that repo's gitignored `.claude/settings.local.json`.

## When to use this

Use this when you want one of this marketplace's plugins in a single repo — to try it before turning it on more widely, or to keep a personal helper here without loading it everywhere.

## Before you start

You need the **plugin name** and this repo's **marketplace name** — the `name` field of `.claude-plugin/marketplace.json`. Together they form the plugin's full id, `plugin-name@marketplace-name`. The plugin lives in `plugins/<name>/` in this repo.

## Steps

These all run in the shell. They do not need an interactive session.

### 1. Make sure the plugin is in the catalog

The marketplace is this repo, and its catalog is `.claude-plugin/marketplace.json`. A plugin is only installable once it has a catalog entry — adding that entry is what makes it available.

Look at `.claude-plugin/marketplace.json`:

- **Already listed** → nothing to do here, move on.
- **Folder exists under `plugins/<name>/` but no catalog entry** → add one. This is the step that makes the plugin installable:

  ```json
  {
    "name": "plugin-name",
    "source": "./plugins/plugin-name",
    "description": "Same one-liner as the plugin's manifest."
  }
  ```

  Append it to `plugins[]`. This is a local edit to this repo — commit it like any other change.
- **No folder at all** → there is nothing to install yet. Create the plugin first (the add-new-plugin skill), then come back.

### 2. Make sure this marketplace is registered

If the marketplace name is not in `claude plugin marketplace list`, add this repo as the source (you only do this once per machine):

```bash
claude plugin marketplace add .
```

Run it from this repo's root so the path resolves to the checkout. The command registers the repo under the `name` declared in `.claude-plugin/marketplace.json`.

If the name is already listed but its source points at a **different** directory, stop and flag it — another marketplace owns that name, and installing would silently resolve against the wrong repo.

### 3. Install at local scope

Run this **from the target repo's root**. Local scope writes relative to the current directory's `.claude/`, so the directory matters.

```bash
claude plugin install plugin-name@marketplace-name --scope local
```

### 4. Seed any required env vars

Some plugins need a secret or setting the user must supply (an API token, for example). Seed a placeholder for each so the user can see exactly what to fill in, instead of hitting a silent failure later.

Look only at the plugin's `.mcp.json` `env` block (in the plugin's source folder, e.g. `plugins/<name>/.mcp.json`). If the plugin has no `.mcp.json`, skip this step.

For each entry in that `env` block, decide if it is a **user input** or **auto-provided**:

- **User input** — the value references its own name, like `"TWITTER_BEARER_TOKEN": "${TWITTER_BEARER_TOKEN:-}"`. These need a real value from the user. Seed them.
- **Auto-provided** — the value only references a `CLAUDE_*` builtin, like `"CACHE_DIR": "${CLAUDE_PLUGIN_DATA}/cache"`. Claude Code fills these in. Skip them.

For each user-input var that is **not already set** in the target `.claude/settings.local.json`, add it under an `env` block with a visible sentinel so the unfinished state is obvious:

```json
{
  "enabledPlugins": { "plugin-name@marketplace-name": true },
  "env": {
    "TWITTER_BEARER_TOKEN": "<set TWITTER_BEARER_TOKEN>"
  }
}
```

Rules:

- **Never overwrite** a value the user already set. Only add missing keys.
- Use the sentinel `"<set NAME>"`, not an empty string, so it reads as "still needs a value."
- These are real secrets. They belong only in the gitignored `settings.local.json`.

## Verify

Confirm the plugin is registered:

```bash
claude plugin list
```

It should appear in `.claude/settings.local.json` (which is gitignored, so it stays on your machine):

```json
{
  "enabledPlugins": {
    "plugin-name@marketplace-name": true
  }
}
```

## Activate

The plugin loads on the **next** session. To apply it in a session that is already running, run `/reload-plugins` or restart Claude Code.

## Remove it

```bash
claude plugin uninstall plugin-name@marketplace-name --scope local
```

## Notes

- Local scope only controls *where the on-switch is written* — the gitignored `.claude/settings.local.json`. It is not a separate copy of the plugin.
- To keep the plugin installed but turn it off, use `claude plugin disable plugin-name@marketplace-name` instead of uninstalling.
