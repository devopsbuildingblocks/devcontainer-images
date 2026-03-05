ARG VARIANT="9"
FROM rockylinux:${VARIANT}
LABEL org.opencontainers.image.source="https://github.com/devopsbuildingblocks/devcontainer-images"

# Install base packages and fix common compatibility issues:
# - Replace curl-minimal with curl (avoids conflicts with devcontainer features)
# - Install glibc-langpack-en for locale support
# - dnf-plugins-core provides `dnf config-manager`, which the
# devcontainers docker-in-docker feature uses to add the Docker CE repository.
RUN dnf install -y --allowerasing \
        util-linux-user \
        git \
        xz \
        curl \
        glibc-langpack-en \
        dnf-plugins-core \
    && dnf clean all

# Set locale (LOCPATH needed for nix-installed programs to find system locales)
ENV LANG=en_US.UTF-8
ENV LC_ALL=en_US.UTF-8
ENV LOCPATH=/usr/lib/locale