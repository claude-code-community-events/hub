---
name: add-event-material
description: >-
  This skill should be used when the user asks to "add event material",
  "submit my slides", "add my talk", "contribute to an event",
  "upload my presentation", "add speaker material", "submit event assets",
  "link my talk repo", "add materials to the event",
  or invokes /add-event-material. Clones the Claude Code Community Events
  hub repo and guides the user through contributing their materials.
disable-model-invocation: true
user-invocable: true
version: 0.1.0
---

# Add Event Material (Plugin)

This skill is the plugin entry point for contributors who do not have the hub repo cloned. It handles getting the repo locally, then defers to the in-repo skill for the actual contribution workflow.

## Workflow

### Step 1: Check if Already in the Hub Repo

Check if the current working directory is already the `claude-code-community-events/hub` repo by looking for `.claude/skills/add-event-material/SKILL.md`.

If found, skip to Step 4 — read and follow that skill directly.

### Step 2: Clone the Hub Repo

Tell the contributor:

> To add your event materials, the hub repo needs to be cloned locally. Where should it go?

Offer these options:
1. **A specific path** — ask them to provide it
2. **Default location** — use `~/repos/claude-code-community-events-hub/`
3. **Temporary** — use the OS temp directory (e.g., `/tmp/claude-code-community-events-hub/` on macOS/Linux)

If the directory already exists and contains the repo (check for `.git/`), skip cloning and use the existing clone. Run a `git pull` to ensure it's up to date.

If the directory doesn't exist, clone:

```bash
git clone https://github.com/claude-code-community-events/hub.git <chosen-path>
```

If the contributor wants to open a PR later (they almost certainly do), they should fork first. Check if `gh` CLI is available and authenticated:

```bash
gh repo fork claude-code-community-events/hub --clone=true --remote=true
```

If `gh` is not available, fall back to a regular clone and remind them they'll need to fork on GitHub before pushing.

### Step 3: Change to the Repo Directory

Change the working directory to the cloned repo:

```bash
cd <chosen-path>
```

### Step 4: Hand Off to the In-Repo Skill

Read the file `.claude/skills/add-event-material/SKILL.md` from the repo and follow the instructions in that file to guide the contributor through the rest of the workflow (determining role, getting event info, scaffolding folders, guiding content, etc.).

The in-repo skill is the source of truth for the contribution workflow. Do not duplicate its logic here.
