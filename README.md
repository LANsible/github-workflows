# github-workflows

### Example

```yaml
---
on:
  - push
  - workflow_dispatch

jobs:
  docker:
    uses: LANsible/github-workflows/.github/workflows/docker-build.yml@main
    with:
      image_name: lansible/home-assistant
      build_args: |
        COMPONENTS=frontend
        OTHER=auth.mfa_modules.totp
    secrets: inherit
```

### Using a package manager cache

The `target=<dir>` must match the `cache_dir` argument to the action to be able to share the cache
```Dockerfile
RUN --mount=type=cache,target=/root/.cache
    pip3 install \
      --user \
      --no-warn-script-location \
      --compile \
      -r requirements.txt \
```

```yaml
---
on:
  - push
  - workflow_dispatch

jobs:
  docker:
    uses: LANsible/github-workflows/.github/workflows/docker-build.yml@main
    with:
      image_name: lansible/home-assistant
      cache_dir: /root/.cache
    secrets: inherit
```
