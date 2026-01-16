# Node.js Baseline

Claude Code permissions template for Node.js/JavaScript/TypeScript projects.

## Allowed Commands

| Command | Purpose |
|---------|---------|
| `npm` | Package management (install, run scripts, etc.) |
| `npx` | Execute npm packages |
| `pnpm` | Fast, disk-efficient package manager |
| `yarn` | Alternative package manager |
| `node` | Run JavaScript directly |
| `bun` | All-in-one JavaScript runtime and toolkit |
| `vitest` | Vite-native testing framework |
| `jest` | JavaScript testing framework |
| `eslint` | JavaScript/TypeScript linter |
| `prettier` | Code formatter |
| `tsc` | TypeScript compiler |
| `tsx` | TypeScript execute - run TS files directly |
| `turbo` | Turborepo monorepo build system |
| `nx` | Nx monorepo build system |
| `playwright` | End-to-end testing framework |
| `cypress` | End-to-end testing framework |
| `biome` | Fast formatter and linter |
| `oxlint` | Oxidation compiler linter |
| `oxc_format` | Oxidation compiler formatter |

## Denied Patterns

| Pattern | Reason |
|---------|--------|
| `.env` | Environment variables often contain secrets |
| `.env.*` | Environment-specific configs (`.env.production`, etc.) |
| `.env.local` | Local overrides (common in Vite/Next.js) |
| `.npmrc` | May contain npm registry auth tokens |
| `secrets/**` | Explicit secrets directory |
| `**/secrets/**` | Nested secrets directories |

## Usage

```bash
mkdir -p .claude
curl -o .claude/settings.json https://raw.githubusercontent.com/YOUR_USERNAME/claude-baseline/main/node/settings.json
```

## Customization Ideas

- Add `webpack`, `vite`, `esbuild`, `rollup` if using those bundlers directly
- Add `prisma`, `drizzle-kit` for database tooling
- Add `storybook` for component development
- Add framework CLIs like `next`, `nuxt`, `astro` if needed
