# SPDX-License-Identifier: MIT
# Original: https://github.com/gitpod-io/workspace-images/blob/961ca52f04e64101a5b362aba106b4ee87b2bd3d/chunks/tool-nix/Dockerfile
ARG base
FROM ${base}

ARG NIX_VERSION
ARG NIX_CONFIG=""

ENV NIX_VERSION=${NIX_VERSION}

# Refer to DL4006 for details.
SHELL [ "/bin/bash", "-o", "pipefail" ]

USER root

# Dazzle does not rebuild a layer until one of its lines are changed. Increase this counter to rebuild this layer.
ENV TRIGGER_REBUILD=1

RUN addgroup --system nixbld \
  && adduser gitpod nixbld \
  && for i in $(seq 1 30); do useradd -ms /bin/bash nixbld$i && adduser nixbld$i nixbld; done \
  && mkdir -m 0755 /nix && chown gitpod /nix \
  && mkdir -p /etc/nix && echo 'sandbox = false' > /etc/nix/nix.conf

# Install Nix
USER gitpod
ENV USER gitpod
WORKDIR /home/gitpod

RUN curl https://nixos.org/releases/nix/nix-$NIX_VERSION/install | sh

RUN echo '. /home/gitpod/.nix-profile/etc/profile.d/nix.sh' >> /home/gitpod/.bashrc.d/200-nix
RUN mkdir -p /home/gitpod/.config/nixpkgs && echo '{ allowUnfree = true; }' >> /home/gitpod/.config/nixpkgs/config.nix
RUN mkdir -p /home/gitpod/.config/nix && echo $NIX_CONFIG >> /home/gitpod/.config/nix/nix.conf

# Install cachix
RUN . /home/gitpod/.nix-profile/etc/profile.d/nix.sh \
  && nix-env -iA cachix -f https://cachix.org/api/v1/install \
  && cachix use cachix

# Install direnv
COPY direnv.config.toml /home/gitpod/.config/direnv/config.toml
RUN echo "source <(direnv hook bash)" | tee /home/gitpod/.bashrc.d/999-direnv \
  && . /home/gitpod/.nix-profile/etc/profile.d/nix.sh \
  && nix-env -iA nixpkgs.direnv

# Finally setup devbox
RUN curl https://get.jetpack.io/devbox | bash -s -- -f
