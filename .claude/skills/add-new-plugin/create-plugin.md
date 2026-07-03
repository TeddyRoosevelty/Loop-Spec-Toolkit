# Add a plugin to this marketplace

**Goal:** put a plugin in this repo's `plugins/` folder so it is available to install — either by authoring a new one or by importing one that already exists in another repo.

**Done when:** `claude plugin validate ./plugins/<name> --strict` passes and the plugin lives in `plugins/<name>/`.

This is a run-book for working in *this* repo. Steps use the CLI and direct file edits.

## Before you start

- The repo is cloned and you are working from its root.
- `npm install` has been run once, so `npm run validate` works.

Use a real name in place of `<name>`. The name is lowercase-kebab, matches the plugin's folder, and becomes its namespace (`/<name>:<skill>`).

## 1. New or import?

Decide how the plugin's folder gets populated:

- **New** — you are authoring it here from scratch. Go to section 2.
- **Import** — the plugin already exists somewhere else and you want it in this marketplace. Go to section 3.

Both paths finish the same way, at section 4.

## 2. Author a new plugin

### Create the manifest

Create `plugins/<name>/.claude-plugin/plugin.json`:

```json
{
  "name": "<name>",
  "description": "One line on what the plugin does.",
  "version": "0.1.0",
  "author": { "name": "TeddyRoosevelty" }
}
```

- `name` must match the folder name.
- `version` must be valid semver (`0.1.0`, not `0.1` or `v0.1.0`).
- `author` is optional.

Only `plugin.json` goes inside `.claude-plugin/`. Everything else sits at the plugin root.

### Add components

Add the parts the plugin ships, each at the plugin root:

- `skills/<skill>/SKILL.md` — see the `/plugin-dev:skill-development` skill.
- `agents/<agent>.md` — see the `/plugin-dev:agent-development` skill.
- `hooks/hooks.json`, `.mcp.json`, etc. — see the matching `plugin-dev` skills.

## 3. Import an existing plugin

### Get the plugin's folder onto disk

The plugin's files live somewhere — get them where you can read them:

- **Already on your machine** (another repo you have checked out) — point at that folder.
- **A git URL** — make a shallow clone into `.pm-data/temp` (gitignored) to read from, and delete it once you have copied what you need.

### Copy it in

Copy the plugin's folder into `plugins/<name>/`, so this repo holds its own self-contained copy. The origin is only where you got it; changes there do not flow back in.

### Reconcile it with this repo

- Set the manifest `name` to match the `<name>` folder (the validators require the folder and manifest name to be the same string).
- Confirm `version` is valid semver.
- **Make it self-contained.** When a plugin is installed, only its own folder travels — the origin repo does not. So nothing inside it may reach outside the plugin folder: no imports from another repo's root or `scripts/`, no dependence on a root `node_modules`, no absolute paths. Vendor any dependency it needs or drop it, and reference files through `${CLAUDE_PLUGIN_ROOT}`. Remove anything tied to its old home.

## 4. Validate and land

Run both checkers:

```bash
claude plugin validate ./plugins/<name> --strict
npm run validate
```

- `claude plugin validate ./plugins/<name> --strict` runs Claude Code's own schema check on the plugin. `--strict` fails on unknown fields and missing metadata. This is the check for the plugin you just added.
- `npm run validate` confirms you haven't broken the existing catalog. It does not check the new plugin yet — that happens once the plugin is listed, at install.

Fix any errors, then commit the new folder.

```bash
git add plugins/<name>
git commit -m "Add <name> plugin"
```

## 5. Smoke-test that it loads (interactive)

`claude --plugin-dir ./plugins/<name>` starts an **interactive** session, so it can't be driven from inside an existing session. Launch it (or restart), then confirm the skill appears and works:

```
/<name>:<skill>
```

## Gotchas

| Symptom | Cause | Fix |
| :-- | :-- | :-- |
| `... name "x" does not match ...` | `plugin.json` name ≠ folder name | Make them the same string |
| `version ... is not valid semver` | Version like `0.1` or `v0.1.0` | Use `MAJOR.MINOR.PATCH` |
| Plugin loads but a shipped script fails | Script reached outside the plugin folder | Make it self-contained; use `${CLAUDE_PLUGIN_ROOT}` |

## Notes

- Leave `marketplace.json` alone — installing the plugin is what lists it there.

## See also

- The `plugin-dev` skills for authoring skills, agents, hooks, and MCP servers.
