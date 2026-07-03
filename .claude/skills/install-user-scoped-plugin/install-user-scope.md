# Install a plugin from this marketplace for yourself across all projects

Turn a plugin from **this marketplace** on for yourself in **every** project on this machine (user scope).

## When to use this

Use this when you want one of this marketplace's plugins available everywhere you work, not tied to one repository.

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

List the marketplaces already registered:

```bash
claude plugin marketplace list
```

If the marketplace name is missing, add this repo as the source (you only do this once per machine):

```bash
claude plugin marketplace add .
```

Run it from this repo's root so the path resolves to the checkout. The command registers the repo under the `name` declared in `.claude-plugin/marketplace.json`.

If the name is already listed but its source points at a **different** directory, stop and flag it — another marketplace owns that name, and installing would silently resolve against the wrong repo.

### 3. Install at user scope

```bash
claude plugin install plugin-name@marketplace-name --scope user
```

User scope is the default, so the `--scope user` flag is optional. Pass it anyway — it makes the command self-documenting and safe if defaults ever change.

### 4. Seed any required env vars

Some plugins need a secret or setting the user must supply (an API token, for example). Seed a placeholder for each so the user can see exactly what to fill in, instead of hitting a silent failure later.

Look only at the plugin's `.mcp.json` `env` block (in the plugin's source folder, e.g. `plugins/<name>/.mcp.json`). If the plugin has no `.mcp.json`, skip this step.

For each entry in that `env` block, decide if it is a **user input** or **auto-provided**:

- **User input** — the value references its own name, like `"TWITTER_BEARER_TOKEN": "${TWITTER_BEARER_TOKEN:-}"`. These need a real value from the user. Seed them.
- **Auto-provided** — the value only references a `CLAUDE_*` builtin, like `"CACHE_DIR": "${CLAUDE_PLUGIN_DATA}/cache"`. Claude Code fills these in. Skip them.

A user-scoped plugin runs in every project, so its env belongs in the same machine-wide file. For each user-input var that is **not already set** in `~/.claude/settings.json`, add it under an `env` block with a visible sentinel:

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
- These are real secrets. `~/.claude/settings.json` is your private machine config, so it is the right place for them.

## Verify

Confirm the plugin is registered:

```bash
claude plugin list
```

It should also appear in `~/.claude/settings.json`:

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
claude plugin uninstall plugin-name@marketplace-name --scope user
```

## Notes

- User scope loads the plugin in *every* project, including ones where you may not want it.
