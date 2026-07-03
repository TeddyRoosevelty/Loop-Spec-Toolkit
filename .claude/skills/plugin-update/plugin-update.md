# Update a plugin and refresh the local install

Bump a plugin's version and refresh this machine's install so it picks up the change.

The one trap: an install's cache only refreshes when the plugin's `version` changes. Edit the code but not the version, and the cache keeps the old copy. Bumping the version is what makes the refresh real.

This is local only. Committing and pushing — so other machines or remote consumers get the change — is separate and not part of this skill.

**this is a fairly mechanical process. Do it fast, quickly.**

## Before you start

- Your change is made and tested under `plugins/<plugin>/`.
- Dev dependencies are installed (`npm install`).

## Steps

### 1. Bump the version

```bash
npm run script bump -- <plugin>            # patch (default)
npm run script bump -- <plugin> --minor    # additive change
npm run script bump -- <plugin> --major    # breaking change
```

This edits only that plugin's `plugins/<plugin>/.claude-plugin/plugin.json`. It does not touch the catalog.

Pick the level by what changed: a fix is a patch, a new feature is a minor, a breaking change is a major.

### 2. Validate

```bash
npm run validate
```

A green run means the version is valid semver and the catalog still lines up. Fix a red run before going on.

### 3. Refresh the local install

```bash
claude plugin marketplace update <marketplace>
claude plugin update <plugin>@<marketplace>
```

`<marketplace>` is this repo's marketplace name — the `name` field of `.claude-plugin/marketplace.json`. Its source on this machine is a directory pointing at the repo, so these commands read the files on disk directly — the bump does not need to be committed for the local refresh to take.

`claude plugin update` refreshes wherever the plugin is installed (user, project, or local scope). If the plugin is not installed on this machine, there is nothing local to refresh — the bump still stands for whenever it is installed.

### 4. Apply

Updates do not apply to a running Claude Code session. After the refresh, **restart Claude Code or run `/reload-plugins`** to load the new version.

## Verify it took

- Read `plugins/<plugin>/.claude-plugin/plugin.json` and confirm the new `version`.
- Run `claude plugin list` and confirm the installed version matches.

## Notes

- **Why bump at all:** the cache only refreshes on a version change. Skip the bump and the install keeps the old copy even after you edit the files.
- **Local plugins only:** `bump` works on plugins whose catalog `source` is a local path (every plugin in this repo). It bails on remote sources.
- **Reaching other consumers:** for machines whose marketplace source is a git clone, the change reaches them when you commit and push the repo — that part is up to you, outside this skill.
