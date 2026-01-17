# GitHub CLI Baseline

Claude Code permissions template for GitHub CLI (`gh`).

## Available Tiers

| File | Use Case |
|------|----------|
| `settings.json` | **Default** — Common PR/issue workflow |
| `settings.readonly.json` | View and explore without changes |
| `settings.full.json` | All gh commands (power users) |

## Tier Comparison

### Pull Requests

| Command | readonly | default | full |
|---------|:--------:|:-------:|:----:|
| `gh pr list`, `view`, `diff` | ✓ | ✓ | ✓ |
| `gh pr checks`, `status` | ✓ | ✓ | ✓ |
| `gh pr create` | | ✓ | ✓ |
| `gh pr checkout`, `merge` | | ✓ | ✓ |
| `gh pr ready`, `review`, `comment` | | ✓ | ✓ |
| `gh pr close`, `reopen`, `edit` | | ✓ | ✓ |

### Issues

| Command | readonly | default | full |
|---------|:--------:|:-------:|:----:|
| `gh issue list`, `view`, `status` | ✓ | ✓ | ✓ |
| `gh issue create` | | ✓ | ✓ |
| `gh issue close`, `reopen` | | ✓ | ✓ |
| `gh issue comment`, `edit` | | ✓ | ✓ |

### Repository

| Command | readonly | default | full |
|---------|:--------:|:-------:|:----:|
| `gh repo view`, `list`, `clone` | ✓ | ✓ | ✓ |
| `gh repo fork` | | ✓ | ✓ |
| `gh repo create` | | | ✓ |
| `gh repo delete` | | | ✓ |
| `gh repo rename`, `edit` | | | ✓ |

### Workflows & Runs

| Command | readonly | default | full |
|---------|:--------:|:-------:|:----:|
| `gh run list`, `view` | ✓ | ✓ | ✓ |
| `gh workflow list`, `view` | ✓ | ✓ | ✓ |
| `gh run watch`, `rerun` | | ✓ | ✓ |
| `gh workflow run` | | ✓ | ✓ |
| `gh workflow enable/disable` | | | ✓ |

### Other

| Command | readonly | default | full |
|---------|:--------:|:-------:|:----:|
| `gh release list`, `view` | ✓ | ✓ | ✓ |
| `gh gist list`, `view` | ✓ | ✓ | ✓ |
| `gh search`, `browse` | ✓ | ✓ | ✓ |
| `gh auth status` | ✓ | ✓ | ✓ |
| `gh release create` | | ✓ | ✓ |
| `gh gist create`, `edit` | | ✓ | ✓ |
| `gh label` | | ✓ | ✓ |
| `gh api` | | | ✓ |
| `gh auth login/logout` | | | ✓ |
| `gh secret`, `variable` | | | ✓ |
| `gh gpg-key`, `ssh-key` | | | ✓ |

## Denied Patterns (All Tiers)

| Pattern | Reason |
|---------|--------|
| `~/.config/gh/**` | GitHub CLI config and OAuth tokens |

## Usage

```bash
mkdir -p .claude

# Default (recommended for most users)
curl -o .claude/settings.json https://raw.githubusercontent.com/YOUR_USERNAME/claude-baseline/main/github/settings.json

# Read-only (for reviewing PRs/issues)
curl -o .claude/settings.json https://raw.githubusercontent.com/YOUR_USERNAME/claude-baseline/main/github/settings.readonly.json

# Full access (power users)
curl -o .claude/settings.json https://raw.githubusercontent.com/YOUR_USERNAME/claude-baseline/main/github/settings.full.json
```

## Why These Tiers?

**readonly** — Best for:
- Reviewing PRs and issues
- Checking CI status
- Exploring repositories
- Triage without making changes

**default** — Best for:
- Day-to-day PR workflow
- Creating and managing issues
- Code review with comments
- Most development workflows

**full** — Best for:
- Repository administration
- Managing secrets and variables
- API scripting with `gh api`
- Auth management

## Combining with Git

GitHub CLI is typically used alongside git:

```bash
# Most projects will want both git/ and github/ permissions
# Merge the allow/deny arrays from both settings files
```

## Security Notes

- `gh api` (full tier only) provides raw API access — very powerful
- `gh auth` commands can modify your authentication
- `gh secret` and `gh variable` can access repository secrets
- Default tier is safe for most collaborative workflows
