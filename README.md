# Podman Desktop Agent Skills extension

<p align="center">
  <img alt="Agent Skills extension icon" src="icon.png" width="128">
</p>

## Overview

This repository contains a minimal Podman Desktop extension scaffold for Agent Skills. It is based on [extension-template-minimal](https://github.com/podman-desktop/extension-template-minimal), at commit [`f5e0579`](https://github.com/podman-desktop/extension-template-minimal/commit/f5e0579a7a9815399116edad18f681621912202d), with the build, lint, typecheck, and CI changes required for this repository.

The extension entrypoint currently only defines empty `activate` and `deactivate` functions. Agent Skills discovery and management are not implemented yet.

See the [Podman Desktop extension documentation](https://podman-desktop.io/docs/extensions) for more information about extension development.

## Development

Prerequisites: Node.js 24 from [`.nvmrc`](.nvmrc) and the pinned pnpm version from [`package.json`](package.json).

1. Clone the repository and install dependencies:

   ```sh
   git clone https://github.com/podman-desktop/extension-agent-skills.git
   cd extension-agent-skills
   nvm use
   corepack enable
   pnpm install --frozen-lockfile
   ```

2. Build the extension. Vite writes the Podman Desktop entrypoint to `dist/extension.cjs`:

   ```sh
   pnpm build
   ```

   To rebuild automatically after source changes:

   ```sh
   pnpm watch
   ```

3. Run the typecheck and linter:

   ```sh
   pnpm typecheck
   pnpm lint:check
   ```

4. Load the extension temporarily in Podman Desktop. Clone Podman Desktop, install its dependencies, and run its development build with this repository as the extension folder. For sibling directories:

   ```sh
   cd ../podman-desktop
   pnpm install
   pnpm watch --extension-folder ../extension-agent-skills
   ```

   Run `pnpm watch` in this repository in a second terminal. Confirm **Agent Skills** appears in Podman Desktop's **Extensions** view.

## Packaging and publishing

The Containerfile builds the extension from source, so a prebuilt `dist/` directory is not required. Build a local OCI image with:

```sh
podman build -t localhost/extension-agent-skills:dev .
```

For publishing instructions, see the [Podman Desktop publishing documentation](https://podman-desktop.io/docs/extensions/publish). The manually dispatched `release` workflow accepts a semantic version and branch, then publishes the image to `ghcr.io/podman-desktop/extension-agent-skills:<version>`. Stable releases also receive the `latest` tag; prereleases do not.
