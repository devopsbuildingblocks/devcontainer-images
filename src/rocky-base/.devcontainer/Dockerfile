ARG VARIANT="9"
FROM rockylinux:${VARIANT}
LABEL org.opencontainers.image.source="https://github.com/devopsbuildingblocks/devcontainer-images"
RUN dnf install -y util-linux-user git xz && dnf clean all
