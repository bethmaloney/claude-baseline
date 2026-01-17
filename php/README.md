# PHP Baseline

Claude Code permissions template for PHP projects.

## Allowed Commands

| Command | Purpose |
|---------|---------|
| `php` | PHP interpreter |
| `composer` | Dependency manager |
| `artisan` / `./artisan` | Laravel CLI |
| `phpunit` | Testing framework |
| `pest` | Testing framework (Laravel-friendly) |
| `phpstan` | Static analysis tool |
| `psalm` | Static analysis tool |
| `pint` | Laravel code style fixer |
| `php-cs-fixer` | PHP Coding Standards Fixer |
| `rector` | Automated refactoring tool |
| `phpcs` / `phpcbf` | PHP CodeSniffer |
| `./vendor/bin/sail` | Laravel Sail (Docker) |

## Denied Patterns

| Pattern | Reason |
|---------|--------|
| `.env` / `.env.*` | Environment variables with secrets |
| `secrets/**` / `**/secrets/**` | Explicit secrets directories |
| `~/.composer/auth.json` | Composer authentication tokens |
| `~/.config/composer/auth.json` | Composer auth (XDG location) |
| `auth.json` | Project-level Composer authentication |

## Usage

```bash
mkdir -p .claude
curl -o .claude/settings.json https://raw.githubusercontent.com/YOUR_USERNAME/claude-baseline/main/php/settings.json
```

## Customization Ideas

- Add `symfony` for Symfony CLI
- Add `wp` for WordPress CLI
- Add `drush` for Drupal CLI
- Add `magento` for Magento CLI
- Add `ddev` for DDEV local development
- Add `valet` for Laravel Valet
- Add `vapor` for Laravel Vapor
- Add `forge` for Laravel Forge CLI
