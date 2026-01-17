# Ruby Baseline

Claude Code permissions template for Ruby and Rails projects.

## Allowed Commands

| Command | Purpose |
|---------|---------|
| `ruby` | Ruby interpreter |
| `gem` | RubyGems package manager |
| `bundle` / `bundler` | Dependency management |
| `rake` | Task runner |
| `rails` / `./bin/rails` | Rails CLI |
| `rspec` / `./bin/rspec` | RSpec testing framework |
| `rubocop` | Linter and formatter |
| `standardrb` | Ruby Standard style guide |
| `erb` | ERB template processor |
| `irb` | Interactive Ruby shell |
| `rdoc` | Documentation generator |
| `yard` | Documentation tool |
| `solargraph` | Language server |
| `spring` | Rails application preloader |
| `foreman` | Procfile-based process manager |
| `kamal` | Deployment tool (formerly MRSK) |
| `cucumber` | BDD testing framework |
| `minitest` | Testing framework |

## Denied Patterns

| Pattern | Reason |
|---------|--------|
| `.env` / `.env.*` | Environment variables with secrets |
| `secrets/**` / `**/secrets/**` | Explicit secrets directories |
| `config/master.key` | Rails encrypted credentials master key |
| `config/credentials/*.key` | Rails environment-specific credential keys |
| `~/.gem/credentials` | RubyGems API key for publishing |

## Usage

```bash
mkdir -p .claude
curl -o .claude/settings.json https://raw.githubusercontent.com/YOUR_USERNAME/claude-baseline/main/ruby/settings.json
```

## Customization Ideas

- Add `hanami` for Hanami framework
- Add `roda` for Roda framework
- Add `sinatra` for Sinatra apps
- Add `puma` / `unicorn` / `falcon` for specific app servers
- Add `sidekiq` for background job runner
- Add `guard` for file watching
- Add `cap` / `capistrano` for deployment
- Add `rbenv` or `rvm` for version management
- Add `steep` / `sorbet` for type checking
