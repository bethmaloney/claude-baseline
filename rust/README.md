# Rust Baseline

Claude Code permissions template for Rust projects.

## Allowed Commands

| Command | Purpose |
|---------|---------|
| `cargo` | Rust's package manager and build tool |
| `rustc` | Rust compiler (direct invocation) |
| `rustup` | Rust toolchain installer and manager |
| `rustfmt` | Code formatter |
| `clippy-driver` | Linter driver |
| `rust-analyzer` | Language server (occasional CLI use) |
| `cargo-watch` | Watch for changes and run commands |
| `cargo-nextest` | Next-generation test runner |
| `cargo-expand` | Expand macros for debugging |
| `cargo-audit` | Audit dependencies for vulnerabilities |
| `cargo-deny` | Lint dependencies for issues |
| `cargo-outdated` | Check for outdated dependencies |
| `cargo-machete` | Find unused dependencies |
| `wasm-pack` | Build Rust-generated WebAssembly |
| `trunk` | WASM web application bundler |

## Denied Patterns

| Pattern | Reason |
|---------|--------|
| `.env` / `.env.*` | Environment variables with secrets |
| `secrets/**` / `**/secrets/**` | Explicit secrets directories |
| `Secrets.toml` / `**/Secrets.toml` | Config-rs secrets file convention |
| `.cargo/credentials.toml` | Cargo registry authentication tokens |
| `~/.cargo/credentials.toml` | Global Cargo credentials |

## Usage

```bash
mkdir -p .claude
curl -o .claude/settings.json https://raw.githubusercontent.com/YOUR_USERNAME/claude-baseline/main/rust/settings.json
```

## Customization Ideas

- Add `diesel` for Diesel CLI migrations
- Add `sqlx` for SQLx CLI
- Add `sea-orm-cli` for SeaORM migrations
- Add `mdbook` for documentation
- Add `cross` for cross-compilation
- Add `cargo-leptos`, `dioxus` for web framework CLIs
