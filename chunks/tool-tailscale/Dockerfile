ARG base
FROM ${base}

USER root

# Dazzle does not rebuild a layer until one of its lines are changed. Increase this counter to rebuild this layer.
ENV TRIGGER_REBUILD=0

# Don't mess up with apt-key, instead use custom sources.list file for Tailscale
# and import the pubkey to /usr/share/keyrings instead.
COPY tailscale.list /etc/apt/sources.list.d/
COPY tailscale-package-repository.gpg /usr/share/keyrings/

RUN apt-get update \
    && apt-get install -y tailscale \
    && rm /etc/apt/sources.list.d/tailscale.list \
    && update-alternatives --set ip6tables /usr/sbin/ip6tables-nft

USER gitpod