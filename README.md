# Devcontainer Images

Reusable devcontainer images published to GitHub Container Registry (ghcr.io). Built using the devcontainer CLI with multi-platform support (linux/amd64, linux/arm64).

## Available Images

All images are available at `ghcr.io/devopsbuildingblocks/devcontainer-images/`

| Image | Description | Current Version |
|-------|-------------|-----------------|
| `ubuntu-base` | Foundation image with build dependencies | 0.1.9 |
| `ubuntu-devbox` | Adds Nix and Devbox package management | 0.1.11 |
| `ubuntu-toolbox` | Adds modern CLI tools | 0.1.3 |
| `ubuntu-toolbox-nf` | Toolbox with Nerd Font icons enabled | 0.1.3 |

### Image Hierarchy

```
ubuntu-base (buildpack-deps:noble-curl)
    └── ubuntu-devbox (adds Nix + Devbox)
        ├── ubuntu-toolbox (adds CLI tools)
        └── ubuntu-toolbox-nf (CLI tools + Nerd Font icons)
```

## Image Details

### ubuntu-base

Foundation image built on `buildpack-deps:noble-curl` with common development utilities.

```json
"image": "ghcr.io/devopsbuildingblocks/devcontainer-images/ubuntu-base:latest"
```

### ubuntu-devbox

Adds Nix package manager and Devbox for reproducible development environments.

```json
"image": "ghcr.io/devopsbuildingblocks/devcontainer-images/ubuntu-devbox:latest"
```

**Included:**
- Nix package manager
- Devbox v0.16.0

### ubuntu-toolbox

Development environment with modern CLI tools for improved productivity.

```json
"image": "ghcr.io/devopsbuildingblocks/devcontainer-images/ubuntu-toolbox:latest"
```

**Included CLI Tools:**
- **oh-my-posh** - Customizable shell prompt
- **eza** - Modern replacement for `ls`
- **bat** - `cat` with syntax highlighting
- **fzf** - Fuzzy finder
- **delta** - Enhanced git diff viewer
- **lazygit** - Terminal UI for git

### ubuntu-toolbox-nf

Same as ubuntu-toolbox but with Nerd Font icons enabled across all tools. Use this if your terminal has a Nerd Font installed.

```json
"image": "ghcr.io/devopsbuildingblocks/devcontainer-images/ubuntu-toolbox-nf:latest"
```

## Usage

### In a devcontainer.json

```json
{
  "name": "My Project",
  "image": "ghcr.io/devopsbuildingblocks/devcontainer-images/ubuntu-toolbox:latest"
}
```

### With a specific version

```json
{
  "image": "ghcr.io/devopsbuildingblocks/devcontainer-images/ubuntu-toolbox:0.1.3"
}
```

## Building Images Locally

This repository includes a devcontainer configuration with all required tools pre-installed via Devbox. Simply open the project in VS Code or any devcontainer-compatible editor and you'll have everything you need.

For local development without devcontainers, install [go-task](https://taskfile.dev/) and [devcontainer CLI](https://github.com/devcontainers/cli).

```bash
# List available images
task list

# Build for native platform
task build IMAGE=ubuntu-base

# Build multi-platform (amd64 + arm64)
task build-multiplatform IMAGE=ubuntu-base

# Push to registry
task push IMAGE=ubuntu-base

# Build and push in one step
task publish IMAGE=ubuntu-base
```

## Versioning

Images use semantic versioning with these tag formats:
- `latest` - Most recent version
- `0` - Major version
- `0.1` - Major.minor version
- `0.1.9` - Full version

Version bumps in `src/<image>/.devcontainer/devcontainer.json` trigger automatic publishing via GitHub Actions.

## Directory Structure

```
src/
├── ubuntu-base/.devcontainer/
│   ├── devcontainer.json
│   └── Dockerfile
├── ubuntu-devbox/.devcontainer/
│   ├── devcontainer.json
│   └── Dockerfile
├── ubuntu-toolbox/.devcontainer/
│   ├── devcontainer.json
│   └── Dockerfile
└── ubuntu-toolbox-nf/.devcontainer/
    ├── devcontainer.json
    └── Dockerfile
```

## License

MIT License - see [LICENSE](LICENSE) for details.
