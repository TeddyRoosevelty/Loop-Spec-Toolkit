# Remove a plugin

Turn a plugin off and take it out of the settings that enable it. Where you remove it depends on where it was turned on.

## When to use this

Use this when you no longer want a plugin loading — in one repo, for the team, or across your machine.

## Before you start

You need the plugin's id, in the form `plugin-name@marketplace-name`, and the **scope** it is enabled at. Read the scope from `claude plugin list`:

```bash
claude plugin list
```

Each entry shows a `Scope` line — `local`, `project`, or `user`. The same plugin can appear at more than one scope; each is a separate on-switch and is removed on its own. Remove the ones you mean to.

## Uninstall vs disable

Two different actions:

- **Uninstall** deletes the enable entry. The setting goes back to clean. Use this when you are done with the plugin here.
- **Disable** keeps the entry but turns it off:

  ```bash
  claude plugin disable plugin-name@marketplace-name
  ```

  Use this when you want to keep it installed and flip it back on later. It earns its keep at user scope, where the plugin is actually downloaded and you want to keep that cache. At local scope the two are nearly the same — both just stop it loading — so prefer uninstall there to leave the file clean.

The rest of this guide covers **uninstall** at each scope.

## Local scope — one repo, just you

The on-switch is one entry in that repo's gitignored `.claude/settings.local.json`. Scope is resolved against the current directory, so this **must run from that repo's root**:

```bash
# from the target repo's root
claude plugin uninstall plugin-name@marketplace-name --scope local
```

Run it from anywhere else and it removes nothing (or removes the plugin from a different repo). Confirm where you are first.

## User scope — every project on your machine

```bash
claude plugin uninstall plugin-name@marketplace-name --scope user
```

This is machine-wide but private to you. It removes the entry from `~/.claude/settings.json`. No commit, no one else affected.

## Project scope — one repo, everyone working in it

Project scope is committed to the repo's `.claude/settings.json`, so removing it is a file edit plus a commit — not a CLI uninstall — and it stops the plugin loading for everyone working in the repo.

### 1. Edit `.claude/settings.json` (the committed file, not `.local`)

Delete the plugin's entry from `enabledPlugins`:

```json
{
  "enabledPlugins": {
    "plugin-name@marketplace-name": true
  }
}
```

Also remove its `extraKnownMarketplaces` block **only if no other enabled plugin uses that marketplace**. If another plugin still comes from it, leave it.

### 2. Commit the change

```bash
git add .claude/settings.json
git commit -m "Remove plugin-name"
```

Committing is what removes the plugin from the repo. Show the change and get approval before you make the commit. Whether and when to push is your normal git workflow.

## Verify

The entry should be gone:

```bash
claude plugin list   # plugin-name@marketplace-name should no longer show at that scope
```

For local scope, the file should be back to having no entry for it:

```bash
cat .claude/settings.local.json
```

## Apply now

Removal takes effect on the **next** session. The plugin keeps loading in a session that is already running until you run `/reload-plugins` or restart Claude Code. For project scope, each person's copy stops loading on their next reload.

## Notes

- **Turn off without removing:** use `claude plugin disable plugin-name@marketplace-name` instead of uninstalling.
- **Removing the marketplace too:** uninstalling a plugin leaves its marketplace registered. To remove that as well (only if nothing else uses it): `claude plugin marketplace remove marketplace-name`.
