ARG base
FROM ${base}

# Refer to DL4006 for details.
SHELL [ "/bin/bash", "-o", "pipefail" ]

USER root

# Dazzle does not rebuild a layer until one of its lines are changed. Increase this counter to rebuild this layer.
ENV TRIGGER_REBUILD=0

# Don't mess up with apt-key, instead use custom sources.list file for Tailscale
# and import the pubkey to /usr/share/keyrings instead.
COPY tailscale.list /etc/apt/sources.list.d/

# hadolint ignore=DL3008
RUN curl -fsSL https://pkgs.tailscale.com/stable/ubuntu/jammy.gpg | gpg --dearmor -o /usr/share/keyrings/tailscale-package-repository.gpg \
    apt-get update \
    && apt-get install -y tailscale \
    && update-alternatives --set ip6tables /usr/sbin/ip6tables-nft

USER gitpod
