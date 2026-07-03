---
description: This skill should be used to add a plugin to this marketplace repository — either authoring a new one or importing an existing one from another repo — so it is available to install. Trigger on requests like "create a new plugin", "add a plugin to this marketplace", "scaffold a plugin named {name}", or "import {plugin} from {repo}". Works only inside this repo. Explicit invocation only.
---

# Add a plugin to this marketplace

## Goal

Put a plugin in this repo's `plugins/{name}/` folder so it is available to install — either by authoring a new one or by importing one that already exists in another repo. End when both validators pass. The full procedure lives in the guide. Read the guide and run it, keeping it as the single source of truth.

**Guide:** [create-plugin.md](./create-plugin.md)

## Confirm before running

First settle whether this is a **new** plugin or an **import** of an existing one, then:

- The **plugin name** (lowercase-kebab; becomes the namespace `/{name}:{skill}`).
- **New** — a one-line description and which components it ships (skills, agents, hooks, MCP servers).
- **Import** — where the existing plugin lives: a folder already on your machine, or a git URL.

Ask for anything the request leaves unclear before starting.

## Process

### 1. Read the guide

Read `create-plugin.md` (in this skill folder) in full for the exact structure, naming rules, and validation commands. Treat it as the source of truth; the steps below only frame how to run it.

### 2. Confirm the inputs, then gate

Settle the new-or-import choice and the name. For a new plugin, also settle the description and component list — and for authoring the components themselves, defer to the `plugin-dev` skills the guide references. For an import, settle where the source lives.

### 3. Preview the plan

State briefly what will happen: the plugin name, whether it is new or imported (and from where), and what lands in `plugins/{name}/`.

### 4. Run the guide

Follow the matching section of the guide — author a new plugin, or import an existing one — then the shared "Validate and land" steps. Validate with both `claude plugin validate ./plugins/{name} --strict` and `npm run validate`. Fix any errors before continuing, then commit the new folder.

### 5. Recap

Report briefly:

- What landed in `plugins/{name}/` (new, or imported from where) and that both validators passed.
- **To smoke-test loading:** `claude --plugin-dir ./plugins/{name}` opens an interactive session. Launching it (or a restart) is the interactive step that remains.
