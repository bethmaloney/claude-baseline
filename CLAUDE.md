# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

claude-baseline is a collection of `.claude/settings.json` templates for different tech stacks — like github/gitignore, but for Claude Code permissions. Each template provides pre-configured `permissions.allow` and `permissions.deny` patterns for a specific technology.

## Repository Structure

```
{stack}/
├── settings.json           # Default balanced permissions
├── settings.readonly.json  # Read-only (optional, for git/github)
├── settings.full.json      # All commands (optional, for git/github)
└── README.md               # Documents what's included and why
```

Directories are organized by language stacks (e.g., node, python, rust) and cross-stack tools (e.g., git, docker).

## Template Format

Each `settings.json` follows this structure:

```json
{
  "permissions": {
    "allow": [
      "Bash(command:*)"
    ],
    "deny": [
      "Read(./.env)",
      "Read(./secrets/**)"
    ]
  }
}
```

- `allow` patterns use `Bash(command:*)` syntax where `*` allows any arguments
- `deny` patterns protect secrets using `Read()` with glob patterns

## Contributing Guidelines

When adding or modifying templates:

1. **Minimal permissions** — Only include commonly-used, safe commands
2. **Always include deny patterns** — Protect secrets specific to that ecosystem
3. **Document non-obvious inclusions** — Explain in the stack's README why each command is included
4. **Follow tier pattern** — For stacks with tiered permissions (readonly/default/full), follow the git/ example

## Permission Tiers

| Tier | File | Use Case |
|------|------|----------|
| readonly | `settings.readonly.json` | Code review, exploration, CI checks |
| default | `settings.json` | Day-to-day development |
| full | `settings.full.json` | Admin tasks, power users |

Currently only `git/` and `github/` have all three tiers.
