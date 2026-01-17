# claude-baseline

A collection of `.claude/settings.json` templates for different tech stacks — like [github/gitignore](https://github.com/github/gitignore), but for Claude Code permissions.

## The Problem

When starting with Claude Code, developers face a choice:

1. **Use `--dangerously-skip-permissions`** — Too risky, bypasses all safety guardrails
2. **Manually configure permissions** — Tedious, easy to miss things, requires deep knowledge of your toolchain
3. **Click "Always allow" repeatedly** — Interrupts flow, no security review

There's no easy way to say "I'm working on a .NET project, give me sensible defaults."

## The Solution

Pre-configured, community-vetted permission templates for common tech stacks:

```
claude-baseline/
├── Language Stacks
│   ├── dotnet/        # .NET/C# development
│   ├── node/          # Node.js/JavaScript/TypeScript
│   ├── python/        # Python development
│   ├── rust/          # Rust development
│   └── go/            # Go development
│
└── Cross-Stack Tools
    ├── git/           # Git version control
    ├── github/        # GitHub CLI (gh)
    └── docker/        # Docker and containers
```

Each template includes:
- **`permissions.allow`** — Safe commands for that ecosystem
- **`permissions.deny`** — Patterns to protect secrets (`.env`, credentials, etc.)

## Permission Tiers

Some stacks offer multiple permission levels:

| File | Purpose |
|------|---------|
| `settings.json` | **Default** — Balanced for common workflows |
| `settings.readonly.json` | Read-only exploration and review |
| `settings.full.json` | All commands (dangerous) |
| `settings.web.json` | Adds WebFetch access to official documentation |

### When to use each tier

| Tier | Best for |
|------|----------|
| **readonly** | Code review, auditing, exploring unfamiliar codebases, CI checks |
| **default** | Day-to-day development, feature work, most workflows |
| **full** | Repository maintenance, admin tasks, power users who understand the risks |
| **web** | When you want Claude to reference official documentation |

Currently, `git/` and `github/` offer readonly/default/full tiers. Most stacks have default and web tiers.

**Note on web tier:** WebFetch allows Claude to read web pages, which introduces prompt injection risk. The `settings.web.json` files only include official documentation domains (e.g., docs.python.org, nodejs.org) to minimize this risk. User-generated content sites are intentionally excluded.

## Usage

1. Find your stack in this repo
2. Copy the `settings.json` to your project's `.claude/settings.json`
3. Customize as needed

```bash
# Example: Setting up a Node.js project
mkdir -p .claude
curl -o .claude/settings.json https://raw.githubusercontent.com/YOUR_USERNAME/claude-baseline/main/node/settings.json
```

### Combining stacks

Most projects need multiple templates. Merge the `allow` and `deny` arrays:

```bash
# A typical full-stack project might combine:
# node/ + git/ + github/ + docker/
```

## Contributing

Contributions welcome! When adding or modifying templates:

1. Keep permissions minimal — only include commonly-used, safe commands
2. Always include deny patterns for secrets specific to that ecosystem
3. Document any non-obvious inclusions in the stack's README
4. Test the configuration in a real project
5. For new stacks with tiered permissions, follow the readonly/default/full pattern

## Philosophy

- **Secure by default** — Deny patterns are as important as allow patterns
- **Minimal permissions** — Include only what's commonly needed
- **Stack-specific** — Each ecosystem has different tools and secrets to protect
- **Composable** — Combine templates for multi-stack projects
- **Community-vetted** — Contributions are reviewed for security

## License

[CC0 1.0 Universal](LICENSE) — Public domain
