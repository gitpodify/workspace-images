ARG base
FROM ${base}

# Refer to DL4006 for details.
SHELL [ "/bin/bash", "-o", "pipefail" ]

USER root

# Dazzle does not rebuild a layer until one of its lines are changed. Increase this counter to rebuild this layer.
ENV TRIGGER_REBUILD=1

# https://docs.docker.com/engine/install/ubuntu/
RUN curl -fsSL https://download.docker.com/linux/ubuntu/gpg | gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg \
    && echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu \
    $(lsb_release -cs) stable" | tee /etc/apt/sources.list.d/docker.list > /dev/null \
    && apt-get update \
    && install-packages docker-ce docker-ce-cli containerd.io docker-buildx-plugin

RUN curl -o /usr/local/bin/docker-compose -fsSL "https://github.com/docker/compose/releases/download/v2.4.1/docker-compose-linux-$(uname -m)" \
    && chmod +x /usr/local/bin/docker-compose && mkdir -p /usr/local/lib/docker/cli-plugins && \
    ln -s /usr/local/bin/docker-compose /usr/local/lib/docker/cli-plugins/docker-compose

# https://github.com/wagoodman/dive
# hadolint disable-DL3015
RUN curl -o /tmp/dive.deb -fsSL https://github.com/wagoodman/dive/releases/download/v0.10.0/dive_0.10.0_linux_amd64.deb \
    && apt-get install --yes /tmp/dive.deb \
    && rm /tmp/dive.deb

USER gitpod
