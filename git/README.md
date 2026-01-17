# Git Baseline

Claude Code permissions template for Git version control.

## Available Tiers

| File | Use Case |
|------|----------|
| `settings.json` | **Default** — Common development workflow |
| `settings.readonly.json` | Explore and review without changes |
| `settings.full.json` | All git commands (power users) |

## Tier Comparison

| Command | readonly | default | full |
|---------|:--------:|:-------:|:----:|
| `status`, `log`, `diff`, `show` | ✓ | ✓ | ✓ |
| `blame`, `shortlog` | ✓ | ✓ | ✓ |
| `branch`, `tag`, `remote` (list) | ✓ | ✓ | ✓ |
| `ls-files`, `rev-parse`, `describe` | ✓ | ✓ | ✓ |
| `config --get/--list` | ✓ | | |
| `config` (all) | | ✓ | ✓ |
| `add`, `commit` | | ✓ | ✓ |
| `push`, `pull`, `fetch` | | ✓ | ✓ |
| `checkout`, `switch`, `restore` | | ✓ | ✓ |
| `merge`, `stash`, `cherry-pick` | | ✓ | ✓ |
| `clean`, `init`, `clone` | | ✓ | ✓ |
| `worktree`, `submodule` | | ✓ | ✓ |
| `reset`, `revert` | | | ✓ |
| `rebase` | | | ✓ |
| `push --force` | | | ✓ |
| `filter-branch`, `reflog` | | | ✓ |

## Denied Patterns (All Tiers)

| Pattern | Reason |
|---------|--------|
| `.git/config` | May contain credentials or sensitive remote URLs |
| `~/.gitconfig` | Global git config with user identity and credentials |
| `~/.git-credentials` | Stored credentials from credential helper |
| `.git-credentials` | Local stored credentials |

## Usage

```bash
mkdir -p .claude

# Default (recommended for most users)
curl -o .claude/settings.json https://raw.githubusercontent.com/YOUR_USERNAME/claude-baseline/main/git/settings.json

# Read-only (for code review/exploration)
curl -o .claude/settings.json https://raw.githubusercontent.com/YOUR_USERNAME/claude-baseline/main/git/settings.readonly.json

# Full access (power users)
curl -o .claude/settings.json https://raw.githubusercontent.com/YOUR_USERNAME/claude-baseline/main/git/settings.full.json
```

## Why These Tiers?

**readonly** — Best for:
- Code review and exploration
- Auditing repositories
- Learning a new codebase
- CI/CD read-only checks

**default** — Best for:
- Day-to-day development
- Feature branches and PRs
- Most development workflows
- Excludes destructive commands like `reset --hard` and `push --force`

**full** — Best for:
- Repository maintenance
- Complex rebasing workflows
- History rewriting (when needed)
- Users who understand git internals

## Security Notes

- Even "readonly" commands like `git branch` can create branches when given arguments
- The default tier excludes `reset`, `rebase`, and force push to prevent accidental history loss
- All tiers protect credential files
