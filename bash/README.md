# Bash Baseline

Claude Code permissions template for standard shell commands.

## Philosophy

Unlike other templates in this repository, Bash only provides a **read-only** tier. This is intentional:

- Shell commands have unbounded scope (entire filesystem)
- Many write operations are irreversible (`rm -rf`)
- The gap between "safe" and "dangerous" is narrow
- Write operations should be approved per-project based on specific needs

## Included Commands

| Command | Purpose |
|---------|---------|
| `ls` | Directory listing |
| `cat`, `head`, `tail` | View file contents |
| `wc` | Word, line, character counts |
| `find`, `grep` | Search files and content |
| `diff` | Compare files |
| `echo` | Output text |
| `jq` | JSON parsing and transformation |

## Not Included

Write operations (`rm`, `mv`, `cp`, `mkdir`, `chmod`, `touch`) and network commands (`curl`, `wget`) are intentionally excluded. Add these per-project if needed.

`env` is also excluded as environment variables often contain sensitive data (API keys, database credentials, tokens). Add per-project if needed after considering what's exposed.

## Usage

```bash
mkdir -p .claude
curl -o .claude/settings.json https://raw.githubusercontent.com/YOUR_USERNAME/claude-baseline/main/bash/settings.json
```
