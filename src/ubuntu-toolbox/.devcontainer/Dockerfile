# Pin to specific version for reproducibility
# Update this version when you want to update the base image
FROM ghcr.io/devopsbuildingblocks/devcontainer-images/ubuntu-base:0.1.0

# Pre-configure Nix for multiplatform builds with QEMU emulation
# This fixes "unable to load seccomp BPF program: Invalid argument" errors
# when building arm64 images on amd64 runners (and vice versa)
RUN mkdir -p /etc/nix \
    && echo "filter-syscalls = false" >> /etc/nix/nix.conf
