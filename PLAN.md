# claude-baseline: Project Plan

## Rationale

### The Gap

Existing Claude Code template repositories focus on:
- Agents and workflows ([davila7/claude-code-templates](https://github.com/davila7/claude-code-templates))
- Skills and commands ([claudekit](https://github.com/claudekit), [awesome-claude-code](https://github.com/hesreallyhim/awesome-claude-code))
- General starter configurations ([serpro69/claude-starter-kit](https://github.com/serpro69/claude-starter-kit))

**None provide gitignore-style, per-stack permission presets.**

Developers currently either:
1. Use `--dangerously-skip-permissions` (unsafe)
2. Manually configure everything (tedious)
3. Repeatedly click "Always allow" (no security review)

### Why This Matters

- **Onboarding friction** — New Claude Code users don't know what commands to allow
- **Security risk** — Without guidance, users either over-permit or accidentally expose secrets
- **Tech stacks have predictable patterns** — A .NET project needs `dotnet build`, a Node project needs `npm install` — this is knowable

## Goals

1. **Reduce friction** — Copy one file, get sensible defaults for your stack
2. **Improve security** — Community-vetted deny patterns protect secrets by default
3. **Be composable** — Combine templates (e.g., `node/` + `docker/` + `github/`)
4. **Stay minimal** — Don't try to be everything; just permissions

## Non-Goals

- Not a replacement for [claude-code-templates](https://github.com/davila7/claude-code-templates) (agents, commands, hooks)
- Not a configuration management tool like [claude-stacks](https://github.com/Commands-com/claude-stacks)
- Not a runtime permission system like [claudeguard](https://github.com/TaroVard/claudeguard)

## Scope (MVP)

### In Scope
- **`allowedTools`** — Per-stack command allowlists
- **`deny` patterns** — Per-stack secret protection

### Out of Scope (for now)
- Hooks
- Custom commands
- CLAUDE.md templates
- Skills
- Auto-detection/setup skill (future)

## Target Tech Stacks (Initial)

| Stack | Key Commands | Secrets to Deny |
|-------|--------------|-----------------|
| **dotnet** | `dotnet restore`, `build`, `test`, `run`, `ef` | `appsettings.*.json`, `user-secrets` |
| **node** | `npm`, `pnpm`, `yarn`, `npx`, `vitest`, `jest` | `.env*`, `.npmrc` |
| **python** | `pip`, `uv`, `pytest`, `ruff`, `python -m` | `.env*`, `settings.py`, `secrets.py` |
| **rust** | `cargo build`, `test`, `run`, `clippy`, `fmt` | `.env*`, `Secrets.toml` |
| **go** | `go build`, `test`, `run`, `mod`, `fmt`, `vet` | `.env*` |
| **java** | `mvn`, `gradle` | `application-*.properties`, `application-*.yml` |
| **docker** | `docker build`, `compose`, `ps`, `logs` | `.env*`, `docker-compose.override.yml` |
| **github** | `gh pr`, `gh issue`, `gh repo` | — |
| **git** | `git status`, `add`, `commit`, `push`, `pull`, `log`, `diff` | — |

## Template Structure

Each stack gets a directory with:

```
{stack}/
├── settings.json    # The actual configuration
└── README.md        # What's included and why (optional)
```

### Example: `node/settings.json`

```json
{
  "permissions": {
    "allow": [
      "Read",
      "Edit",
      "Write",
      "Bash(npm:*)",
      "Bash(npx:*)",
      "Bash(pnpm:*)",
      "Bash(yarn:*)",
      "Bash(node:*)",
      "Bash(vitest:*)",
      "Bash(jest:*)",
      "Bash(eslint:*)",
      "Bash(prettier:*)",
      "Bash(tsc:*)"
    ],
    "deny": [
      "Read(./.env)",
      "Read(./.env.*)",
      "Read(./.npmrc)",
      "Read(./secrets/**)"
    ]
  }
}
```

## Future Considerations

### Auto-Detection Skill
A Claude Code skill that:
1. Detects project type (package.json → node, .csproj → dotnet, etc.)
2. Suggests or applies the appropriate baseline
3. Allows combining multiple stacks

### Composability
Allow users to easily combine templates:
```bash
# Hypothetical future CLI
claude-baseline init node docker github
```

### Community Contributions
- Clear contribution guidelines
- Security review process for new templates
- Versioning strategy (if commands/patterns change)

## Known Challenges

1. **Deny pattern bugs** — There are [reported issues](https://github.com/anthropics/claude-code/issues/6699) with deny patterns not being consistently enforced
2. **Settings hierarchy** — Users need to understand project vs. user vs. local settings
3. **Version drift** — Tool flags and patterns may change over time

## Success Metrics

- Adoption: GitHub stars, forks, usage
- Contributions: Community-submitted stacks
- Feedback: Issues, discussions about improvements
- Impact: Reduction in `--dangerously-skip-permissions` usage (anecdotal)

## References

- [Claude Code Settings Docs](https://code.claude.com/docs/en/settings)
- [github/gitignore](https://github.com/github/gitignore) — Inspiration for structure
- [Known deny pattern issues](https://github.com/anthropics/claude-code/issues/6699)
