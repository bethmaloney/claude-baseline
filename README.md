# claude-baseline

Pre-configured Claude Code permissions for common tech stacks. Like [github/gitignore](https://github.com/github/gitignore), but for Claude Code.

## Quick Start

```bash
claude plugin marketplace add bethmaloney/claude-baseline
claude plugin install baseline-permissions@claude-baseline
```

Then in any project:
```
/baseline-permissions
```

That's it. The plugin detects your tech stack and configures `.claude/settings.json`.

---

## What This Solves

Without sensible defaults, you're stuck with:
- **`--dangerously-skip-permissions`** — Too risky
- **Manual configuration** — Tedious, error-prone
- **Clicking "Always allow" repeatedly** — Interrupts flow

This gives you vetted permission templates for Node, Python, Rust, Go, .NET, Docker, Git, and more.

## Available Stacks

| Stack | Description |
|-------|-------------|
| `node` | npm, yarn, pnpm, bun, jest, vitest, eslint, prettier, tsc |
| `python` | pip, uv, pytest, ruff, black, mypy, poetry |
| `go` | go, gofmt, golangci-lint |
| `rust` | cargo, rustc, rustfmt, clippy |
| `dotnet` | dotnet, nuget, msbuild |
| `java` | maven, gradle |
| `ruby` | bundler, rake, rspec, rubocop |
| `php` | composer, phpunit, phpstan |
| `cpp` | cmake, make, gcc, clang |
| `docker` | docker, docker-compose |
| `git` | status, log, diff, commit, push, pull |
| `github` | gh pr, gh issue, gh repo |

## Permission Tiers

| Tier | File | Use Case |
|------|------|----------|
| `standard` | `settings.json` | Day-to-day development (default) |
| `readonly` | `settings.readonly.json` | Code review, exploration |
| `full` | `settings.full.json` | Admin tasks, power users |
| `web` | `settings.web.json` | Adds official docs access |

The plugin prompts you to choose.

## Manual Setup

If you prefer not to use the plugin:

```bash
mkdir -p .claude
curl -o .claude/settings.json https://raw.githubusercontent.com/bethmaloney/claude-baseline/main/node/settings.json
```

Combine multiple stacks by merging the `allow` and `deny` arrays.

## Philosophy

- **Secure by default** — Deny patterns are as important as allow patterns
- **Minimal permissions** — Include only what's commonly needed
- **Stack-specific** — Each ecosystem has different tools and secrets to protect
- **Composable** — Combine templates for multi-stack projects
- **Community-vetted** — Contributions are reviewed for security

## Contributing

1. Keep permissions minimal
2. Always include deny patterns for secrets
3. Update `index.json` with detection patterns
4. Test in a real project

## License

[CC0 1.0 Universal](LICENSE) — Public domain
