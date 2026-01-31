# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Repository Purpose

This repository contains reusable devcontainer images published to GitHub Container Registry (ghcr.io). Images are built using the devcontainer CLI and support multi-platform builds (linux/amd64, linux/arm64).

## Build Commands

Build a specific image for native platform:
```bash
task build IMAGE=<image-name>
```

Build multi-platform image:
```bash
task build-multiplatform IMAGE=<image-name>
```

Push an image:
```bash
task push IMAGE=<image-name>
```

Build and push in one step:
```bash
task publish IMAGE=<image-name>
```

List available images:
```bash
task list
```

## Image Hierarchy

Images build upon each other in this dependency chain:

```
ubuntu-base (buildpack-deps:noble-curl)
    └── ubuntu-devbox (adds Nix + Devbox)
        ├── ubuntu-toolbox (adds CLI tools: oh-my-posh, eza, bat, fzf, delta, lazygit)
        └── ubuntu-toolbox-nf (same as toolbox but with Nerd Font icons enabled)
```

## Versioning and Publishing

- Each image version is defined in its `src/<image>/devcontainer.json` under the `version` field
- Bumping the version triggers automatic publishing via GitHub Actions when merged to main
- The CI workflow automatically detects version changes, sorts images by dependency order, and builds/publishes them
- Semantic version tags are applied: `latest`, major (`1`), major.minor (`1.2`), and full version (`1.2.3`)
- Manual publishing is available via workflow dispatch with control over which tags to apply

## Directory Structure

- `src/<image-name>/.devcontainer/` - Contains `devcontainer.json` and `Dockerfile` for each image
- Features are pulled from `ghcr.io/devopsbuildingblocks/devcontainer-features/`
