# Contribution Guidelines + Docs for Contributors

## Before you start

While the workspace images we maintain here are probably different from [the upstream](https://github.com/gitpod-io/workspace-images), we're currently
limited to the tools and languages that we at Recap Time Squad use in our daily work. If you think that bringing a tool here would be more
suitable for everyone, we may suggest to submit it to upstream's issue tracker for consideration.

If you still want to add a new image here, it's often required to get an acknowledgement from the maintainers by filling a new ticket in our GitLab (or
GitHub) issue tracker so that we can assess if we have the enough bandwidth to maintain the image.

While using Gitpod is often the preferred way to setup your developer environment without cluttering your local setup
and to easily contribute to the project,
we also have configurations for both Dev Containers and GitHub Codespaces if you prefer those.

Maintainers have access to push branches to this repo whereas the community is expected to fork this repo in order to raise a merge request to keep things
less cluttered.

## Tools

> **Warning**: If you proceed with Devbox, please be reminded that we'll be working on a workaround to make Dazzle installable via nix flakes.

If you want a nix-based hybrid dev env setup, consider using [`devbox`](https://jetpack.io/devbox/docs/contributor-quickstart/) and just run `devbox shell`
(or use its [VS Code extension](https://www.jetpack.io/devbox/docs/ide_configuration/vscode/)).

If you prefer to set things up manually, you need:

1. Docker Engine (Linux-only) or Docker Desktop (Windows, macOS, Linux) to run a local container registry for build caching.
2. The [buildkitd binary](https://github.com/moby/buildkit), as used by Dazzle
3. The [Dazzle CLI (and its companion utility program)](https://github.com/gitpod-io/dazzle/) itself, primarily to build the images.

Optionally, you also need:

* Hadolint and ShellCheck for linting shell scripts and Dockerfiles in VS Code

## Building images

We use the `build-*.sh` scripts from the upstream and condense them into one script for easy maintainability, as maintained in the `dazzle-build-script`
repository.
