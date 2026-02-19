# Use latest stable Go version
FROM golang:1.26.0-alpine

# Replace deprecated MAINTAINER with LABEL
LABEL org.opencontainers.image.title="Go CI/CD Environment"
LABEL org.opencontainers.image.description="Lightweight Go development and CI/CD environment"
LABEL org.opencontainers.image.authors="Anmol Nagpal <anmol@clouddrove.com>"
LABEL org.opencontainers.image.source="https://github.com/anmolnagpal/dockerfiles"

# Install build dependencies in a single layer and clean up
RUN set -eux; \
    apk add --no-cache \
        make \
        curl \
        bash \
        gcc \
        musl-dev \
        openssl \
        git \
        ca-certificates && \
    rm -rf /var/cache/apk/*

# Create non-root user for security
RUN addgroup -g 1001 gouser && \
    adduser -D -u 1001 -G gouser gouser

# Set working directory
WORKDIR /workspace

# Change ownership of workspace
RUN chown gouser:gouser /workspace

# Switch to non-root user
USER gouser

# Health check to verify Go environment is working
HEALTHCHECK --interval=30s --timeout=3s --start-period=5s --retries=3 \
    CMD go version || exit 1

# Set default command
CMD ["/bin/bash"]