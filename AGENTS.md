# AGENTS.md

## Project Overview

Podman Desktop Agent Skills extension based on the minimal extension template,
with a Vite build and shared Podman Desktop repository tooling.

- **Tech stack**: TypeScript, Node.js 24, pnpm, Vite
- **Extension API**: `@podman-desktop/api`
- **Main entrypoint**: `src/extension.ts`
- **Built entrypoint**: `dist/extension.cjs`

## Quick Start

```sh
nvm use
corepack enable
pnpm install --frozen-lockfile
pnpm build
```

## Essential Commands

```sh
pnpm build       # bundle the extension into dist/
pnpm watch       # rebuild the extension when source files change
pnpm typecheck   # run TypeScript without emitting files
pnpm lint:check  # run ESLint
```

## Single-File Verification

```sh
pnpm exec eslint path/to/file.ts
pnpm typecheck
```

## Architecture

- `src/extension.ts` exports the `activate` and `deactivate` lifecycle functions.
  They are currently empty; Agent Skills features are not implemented yet.
- `package.json` `contributes` section defines commands/menus/views.
- Vite bundles the extension as `dist/extension.cjs`, loaded by Podman Desktop.

## Pattern References

- Add a command: `package.json` `contributes.commands` + handler in `src/extension.ts`
- Add menu item: `package.json` `contributes.menus` + command implementation
- Add config key: `package.json` `contributes.configuration`
