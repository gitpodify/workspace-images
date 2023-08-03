# Chunk tests for Dazzle

Treat these YAMl files like unit tests, but for Dazzle image chunks after they're being built.

## Setting up for a new chunk

As you run `scripts/new-chunk`, you should see the following prompt to edit your new `<tool|lang>-<chunk-name>.yaml` file
on your editor, similar to this:

```output
gitpod /workspace/workspace-images (main) $ ./scripts/new-chunk tool-gitlab-cli
Checking if directory exists...ok (doesn't exist yet)
Creating needed chunk directory...done
Copying template Dockerfile to chunks/tool-gitlab-cli/Dockerfile...done
Copying template tests YAML file to tests/tool-gitlab-cli.yaml...done
prompt: Does it need to build this chunk for more than one version is popular? [y/N]: N

==========

Setup done! Please edit your chunk's Dockerfile and its corresponding
test YAML file in the tests folder before you run the build script(s).
```

Find your chunk's test file here and edit as needed. In most cases, you usually need to
check the version first or just check if it's reachable by `$PATH`.

```yaml
# copied from tool-tailscale.yaml file
- desc: tailscale should be installed
  command: ["command", "-v", "tailscale"]
  assert:
  - status == 0
  - stdout.indexOf("/bin/tailscale") != -1
- desc: it should find tailscale.list
  command: [wc,/etc/apt/sources.list.d/tailscale.list]
  assert:
  - status == 0
```
