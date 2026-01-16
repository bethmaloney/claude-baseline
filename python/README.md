# Python Baseline

Claude Code permissions template for Python projects.

## Allowed Commands

| Command | Purpose |
|---------|---------|
| `python` / `python3` | Python interpreter |
| `pip` / `pip3` | Package installer |
| `uv` | Fast Python package installer and resolver |
| `poetry` | Dependency management and packaging |
| `pdm` | Modern Python package manager |
| `hatch` | Modern Python project manager |
| `pytest` | Testing framework |
| `tox` | Test automation and virtualenv management |
| `ruff` | Fast Python linter and formatter |
| `black` | Code formatter |
| `isort` | Import sorter |
| `flake8` | Linting tool |
| `pylint` | Static code analyzer |
| `mypy` | Static type checker |

## Denied Patterns

| Pattern | Reason |
|---------|--------|
| `.env` / `.env.*` | Environment variables with secrets |
| `.pypirc` | PyPI credentials for package publishing |
| `secrets/**` | Explicit secrets directory |
| `secrets.py` / `**/secrets.py` | Common pattern for storing secrets in code |
| `config/settings.py` | Often contains sensitive configuration |
| `local_settings.py` | Django pattern for local overrides with secrets |
| `**/local_settings.py` | Nested local settings files |
| `.secrets.toml` | Dynaconf secrets file |

## Usage

```bash
mkdir -p .claude
curl -o .claude/settings.json https://raw.githubusercontent.com/YOUR_USERNAME/claude-baseline/main/python/settings.json
```

## Customization Ideas

- Add `django-admin`, `flask`, `fastapi` for framework CLIs
- Add `celery` for task queue management
- Add `alembic` for database migrations
- Add `jupyter`, `ipython` for notebook development
- Add `sphinx`, `mkdocs` for documentation generation
