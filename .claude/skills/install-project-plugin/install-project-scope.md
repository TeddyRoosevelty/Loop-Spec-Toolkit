# Add a plugin from this marketplace to a project

Make a plugin from **this marketplace** part of a repository so everyone working in that repo gets it — no per-person setup (project scope).

## When to use this

Use this when one of this marketplace's plugins should load for everyone on a repo, not just you.

## Before you start

You need:

- The **plugin name** and this repo's **marketplace name** — the `name` field of `.claude-plugin/marketplace.json`. Together they form the plugin's full id, `plugin-name@marketplace-name`. The plugin lives in `plugins/<name>/` in this repo.
- The **target repo** — the one whose committed `.claude/settings.json` you'll edit. Most often that is this marketplace repo itself.

## Steps

For a plugin to load for the project, the repo's committed `.claude/settings.json` must say two things: **where** to get it (the marketplace, under `extraKnownMarketplaces`) and **which** plugin to turn on (under `enabledPlugins`).

### 1. Make sure the plugin is in the catalog

The marketplace is this repo, and its catalog is `.claude-plugin/marketplace.json`. A plugin is only installable once it has a catalog entry — adding that entry is what makes it available.

Look at `.claude-plugin/marketplace.json`:

- **Already listed** → move on.
- **Folder exists under `plugins/<name>/` but no catalog entry** → add one. This is the step that makes the plugin installable:

  ```json
  {
    "name": "plugin-name",
    "source": "./plugins/plugin-name",
    "description": "Same one-liner as the plugin's manifest."
  }
  ```

  Append it to `plugins[]`. It is a plain local edit to this repo.
- **No folder at all** → there is nothing to install yet. Create the plugin first (the add-new-plugin skill), then come back.

### 2. Edit `.claude/settings.json` (the committed file, not `.local`)

Add both blocks. If the file already has other settings, merge these keys in — do not overwrite what is there. `marketplace-name` is the `name` from `.claude-plugin/marketplace.json` — both the `extraKnownMarketplaces` key and the suffix of the `enabledPlugins` id must match it exactly.

```json
{
  "extraKnownMarketplaces": {
    "marketplace-name": {
      "source": { "source": "directory", "path": "." }
    }
  },
  "enabledPlugins": {
    "plugin-name@marketplace-name": true
  }
}
```

The directory source `{ "source": "directory", "path": "." }` points at this repo's checkout, so no separate copy is fetched and the install tracks the checked-out commit. Use this when the marketplace lives in the **same repo** receiving the settings — the common case.

Both settings are **object maps**, not arrays. The `enabledPlugins` key is the full `plugin-name@marketplace-name` id; the value `true` enables it (`false` would install it but leave it off).

### 3. Commit the change

```bash
git add .claude/settings.json
git commit -m "Enable plugin-name for the project"
```

Committing is what makes the plugin part of the repo. Whether and when to push is your normal git workflow — this skill does not handle it.

### 4. Seed any required env vars (in the gitignored file, never the commit)

Some plugins need a secret the user must supply (an API token, for example). A secret must **never** go in the committed `.claude/settings.json`. It belongs only in each person's gitignored `.claude/settings.local.json`.

Look only at the plugin's `.mcp.json` `env` block (in the plugin's source folder, e.g. `plugins/<name>/.mcp.json`). If the plugin has no `.mcp.json`, skip this step.

For each entry in that `env` block, decide if it is a **user input** or **auto-provided**:

- **User input** — the value references its own name, like `"TWITTER_BEARER_TOKEN": "${TWITTER_BEARER_TOKEN:-}"`. These need a real value from the user. Seed them.
- **Auto-provided** — the value only references a `CLAUDE_*` builtin, like `"CACHE_DIR": "${CLAUDE_PLUGIN_DATA}/cache"`. Claude Code fills these in. Skip them.

For each user-input var that is **not already set**, add it to your own `.claude/settings.local.json` (the gitignored file, **not** the committed `settings.json`) with a visible sentinel:

```json
{
  "env": {
    "TWITTER_BEARER_TOKEN": "<set TWITTER_BEARER_TOKEN>"
  }
}
```

Rules:

- **Only the committed file is shared.** The secret stays in `settings.local.json`, which is gitignored, so it gets the plugin working for **you** without leaking.
- Because the secret cannot ride along in the commit, **each person sets their own** the same way. The committed change enables the plugin; it cannot supply the secret.
- **Never overwrite** a value already set. Use the sentinel `"<set NAME>"`, not an empty string.

## Verify

After a restart or reload, from the repo:

```bash
claude plugin marketplace list   # marketplace-name should be listed
claude plugin list               # should show plugin-name@marketplace-name under project scope, enabled
```

## Activate

The plugin loads on the **next** session. To apply it in a session that is already running, run `/reload-plugins` or restart Claude Code.

## Remove it

Delete the plugin's `enabledPlugins` entry from `.claude/settings.json` (and the `extraKnownMarketplaces` block if nothing else uses it), then commit.

## Notes

- **Opting out:** anyone can turn the plugin off just for themselves with `claude plugin disable plugin-name@marketplace-name`, or a `false` entry in their own `.claude/settings.local.json`. Project scope does not mean forced.
- **Nothing loads until trusted:** this plugin, like all project settings, only takes effect after the folder is trusted.
