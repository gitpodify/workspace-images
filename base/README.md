# Base Dazzle image

Based off [upstream's Dockerfile](https://github.com/gitpod-io/workspace-images/blob/6e94c2184c21cd3aa1f1343d45253850eecaff32/base/Dockerfile), with
some customizations on the global gitconfig.

## Usage

```docker
# DO NOT USE BUILD ARGUMENTS LIKE THIS IF YOU'RE ALSO USING DAZZLE TOO, ESPECIALLY
# IN THIS REPO. HARD CODE THEM INSTEAD.

ARG REGISTRY=ghcr.io/gitpodify/workspace-images # also dock.mau.dev/gitpodify/workspace-images OR quay.io/gitpodified-workspace-images
FROM ${REGISTRY}/base:latest

# the rest of your dockerfile
```

```yaml
image: ghcr.io/gitpodify/workspace-images/base:latest
```
