# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

claude-baseline is a collection of `.claude/settings.json` templates for different tech stacks — like github/gitignore, but for Claude Code permissions. Each template provides pre-configured `permissions.allow` and `permissions.deny` patterns for a specific technology.

## Repository Structure

```
├── index.json              # Stack index with metadata, tiers, and detection patterns
├── skill/                  # Installable skill for auto-configuration
│   └── baseline-permissions/
│       └── SKILL.md
└── {stack}/
    ├── settings.json           # Default balanced permissions
    ├── settings.readonly.json  # Read-only (optional, for git/github)
    ├── settings.full.json      # All commands (optional, for git/github)
    ├── settings.web.json       # Adds WebFetch for official documentation
    └── README.md               # Documents what's included and why
```

Directories are organized by language stacks (e.g., node, python, rust) and cross-stack tools (e.g., git, docker).

## Index File

The `index.json` at the repo root provides machine-readable metadata for all stacks:

```json
{
  "stacks": {
    "node": {
      "description": "Node.js/TypeScript: npm, yarn, pnpm, bun, jest, vitest, eslint, prettier, tsc",
      "tiers": ["standard", "web"],
      "detect": ["package.json", "yarn.lock", "pnpm-lock.yaml"]
    },
    "git": {
      "description": "Git: status, log, diff, commit, push, pull",
      "tiers": ["readonly", "standard", "full", "web"],
      "detect": [".git"]
    }
  },
  "files": {
    "readonly": "settings.readonly.json",
    "standard": "settings.json",
    "full": "settings.full.json",
    "web": "settings.web.json"
  }
}
```

When adding a new stack, update `index.json` with:
- `description`: Human-readable summary of included tools
- `tiers`: Array of available permission tiers
- `detect`: Files/patterns that indicate this stack is present in a repo

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
| web | `settings.web.json` | Allows WebFetch to official documentation |

Currently only `git/` and `github/` have readonly/default/full tiers. The `web` tier is available for all stacks.

**Note on web tier:** WebFetch allows Claude to read web pages, which introduces prompt injection risk. The `settings.web.json` files only include official documentation domains (e.g., docs.python.org, nodejs.org) to minimize this risk. User-generated content sites are intentionally excluded.
