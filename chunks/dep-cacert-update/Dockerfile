ARG base
FROM ${base}

USER gitpod

# Dazzle does not rebuild a layer until one of its lines are changed. Increase this counter to rebuild this layer.
ENV TRIGGER_REBUILD=0

# hadolint ignore=DL3004
RUN sudo apt-get install -y --only-upgrade ca-certificates
