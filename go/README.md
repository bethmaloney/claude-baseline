# Go Baseline

Claude Code permissions template for Go projects.

## Allowed Commands

| Command | Purpose |
|---------|---------|
| `go` | Go toolchain (build, test, run, mod, fmt, vet, etc.) |
| `gofmt` | Code formatter |
| `goimports` | Format and manage imports |
| `golint` | Linter (deprecated but still used) |
| `golangci-lint` | Meta-linter aggregating many linters |
| `staticcheck` | Static analysis tool |
| `govulncheck` | Vulnerability scanner for dependencies |
| `gotests` | Generate table-driven tests |
| `mockgen` | Generate mocks for interfaces |
| `wire` | Compile-time dependency injection |
| `swag` | Swagger documentation generator |
| `air` | Live reload for development |
| `templ` | Type-safe HTML templating |
| `dlv` | Delve debugger |

## Denied Patterns

| Pattern | Reason |
|---------|--------|
| `.env` / `.env.*` | Environment variables with secrets |
| `secrets/**` / `**/secrets/**` | Explicit secrets directories |
| `.netrc` / `~/.netrc` | Network credentials (used by `go get` for private repos) |

## Usage

```bash
mkdir -p .claude
curl -o .claude/settings.json https://raw.githubusercontent.com/YOUR_USERNAME/claude-baseline/main/go/settings.json
```

## Customization Ideas

- Add `migrate` for golang-migrate database migrations
- Add `goose` for Goose migrations
- Add `ent` for Ent ORM codegen
- Add `sqlc` for SQL-to-Go codegen
- Add `buf` for Protocol Buffers
- Add `ko` for building container images
- Add `goreleaser` for release automation
