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
├── dotnet/
│   └── settings.json      # dotnet build, test, ef migrations, etc.
├── node/
│   └── settings.json      # npm/pnpm/yarn, vitest, eslint, etc.
├── python/
│   └── settings.json      # pip, pytest, uv, ruff, etc.
├── rust/
│   └── settings.json      # cargo build, test, clippy, etc.
├── go/
│   └── settings.json      # go build, test, mod tidy, etc.
└── ...
```

Each template includes:
- **`permissions.allow`** — Safe commands for that ecosystem
- **`permissions.deny`** — Patterns to protect secrets (`.env`, credentials, etc.)

## Usage

1. Find your stack in this repo
2. Copy the `settings.json` to your project's `.claude/settings.json`
3. Customize as needed

```bash
# Example: Setting up a Node.js project
mkdir -p .claude
curl -o .claude/settings.json https://raw.githubusercontent.com/YOUR_USERNAME/claude-baseline/main/node/settings.json
```

## Contributing

Contributions welcome! When adding or modifying templates:

1. Keep permissions minimal — only include commonly-used, safe commands
2. Always include deny patterns for secrets specific to that ecosystem
3. Document any non-obvious inclusions
4. Test the configuration in a real project

## Philosophy

- **Secure by default** — Deny patterns are as important as allow patterns
- **Minimal permissions** — Include only what's commonly needed
- **Stack-specific** — Each ecosystem has different tools and secrets to protect
- **Community-vetted** — Contributions are reviewed for security

## License

[CC0 1.0 Universal](LICENSE) — Public domain, same as github/gitignore
