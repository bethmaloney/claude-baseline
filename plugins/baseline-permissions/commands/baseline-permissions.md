---
name: baseline-permissions
description: Configure Claude Code permissions for a repository. Use when users invoke /baseline-permissions, ask to "set up permissions", "configure allow lists", or want to add Claude Code permissions to their project. Automatically detects tech stacks (node, python, go, rust, etc.) or accepts manual specification. Prompts for permission tier and optional web access.
---

# Baseline Permissions

Configure `.claude/settings.json` with pre-built permission allow lists for detected or specified tech stacks.

**Source repo:** https://github.com/bethmaloney/claude-baseline

## Workflow

### Step 1: Fetch Index

Fetch the stack index:
```bash
curl -sf https://raw.githubusercontent.com/bethmaloney/claude-baseline/main/index.json
```

The index contains:
- `stacks.<name>.description` - Human-readable description
- `stacks.<name>.tiers` - Available permission tiers (e.g., `["standard", "web"]` or `["readonly", "standard", "full", "web"]`)
- `stacks.<name>.detect` - Files/patterns that indicate this stack is present
- `files` - Mapping of tier names to settings filenames

### Step 2: Detect or Select Stacks

**If user specified stacks** (e.g., "set up permissions for node and python"):
- Validate against index, use those stacks directly

**Otherwise**, detect stacks using Glob tool:

For each stack in the index, check if any of its `detect` patterns exist:
- Use `Glob(pattern)` for each detection file
- If any match, that stack is detected

Example detection checks:
- `node`: Glob for `package.json`, `yarn.lock`, `pnpm-lock.yaml`
- `python`: Glob for `pyproject.toml`, `requirements.txt`, `Pipfile`
- `go`: Glob for `go.mod`
- `rust`: Glob for `Cargo.toml`
- `git`: Check if `.git` directory exists
- `docker`: Glob for `Dockerfile`, `docker-compose.yml`

Present detected stacks to user for confirmation. If none detected or user wants different ones, use AskUserQuestion with multiSelect, building options from the index's stack descriptions.

### Step 3: Select Permission Tier

Check which tiers are available for ALL selected stacks (intersection of each stack's `tiers` array). Use AskUserQuestion:

```
question: "What permission level do you want?"
header: "Tier"
options:
  - label: "Standard (Recommended)"
    description: "Common dev commands: build, test, lint, format. Good balance of convenience and safety."
  - label: "Read-only"
    description: "Only status/inspection commands. For code review or exploration."
  - label: "Full"
    description: "All commands for that tool. Maximum convenience, less restrictive."
```

Only show readonly/full options if ALL selected stacks support them.

### Step 4: Web Access (Documentation)

Use AskUserQuestion:

```
question: "Enable web access for official documentation?"
header: "Web"
options:
  - label: "No (Recommended)"
    description: "No web fetch. Safest option."
  - label: "Yes"
    description: "Allow fetching official docs (e.g., docs.python.org). Increases prompt injection risk."
```

### Step 5: Fetch Settings from Remote

**Base URL:** `https://raw.githubusercontent.com/bethmaloney/claude-baseline/main`

Use the `files` mapping from index:
- `readonly` → `settings.readonly.json`
- `standard` → `settings.json`
- `full` → `settings.full.json`
- `web` → `settings.web.json`

For each selected stack, fetch via curl:
```bash
curl -sf https://raw.githubusercontent.com/bethmaloney/claude-baseline/main/{stack}/settings.json
```

If web enabled, also fetch:
```bash
curl -sf https://raw.githubusercontent.com/bethmaloney/claude-baseline/main/{stack}/settings.web.json
```

### Step 6: Merge Permissions

Combine all fetched settings:
1. Collect all `permissions.allow` arrays
2. Collect all `permissions.deny` arrays
3. Deduplicate and sort alphabetically

### Step 7: Update Target Settings

Read existing `.claude/settings.json` if it exists (preserve other settings).

Merge permissions:
- Add new `allow` entries (deduplicate)
- Add new `deny` entries (deduplicate)

If `.claude/` directory doesn't exist, create it.

Write final settings with 2-space indent JSON formatting.

## Example Output

Node + Python with standard tier and web enabled:

```json
{
  "permissions": {
    "allow": [
      "Bash(node:*)",
      "Bash(npm:*)",
      "Bash(pip:*)",
      "Bash(pytest:*)",
      "Bash(python:*)",
      "WebFetch(domain:docs.python.org)",
      "WebFetch(domain:nodejs.org)"
    ],
    "deny": [
      "Read(./.env)",
      "Read(./.env.*)",
      "Read(./secrets/**)"
    ]
  }
}
```
