# Docker Build Push Action

A modified version of [docker-build-push-action](https://github.com/docker/build-push-action) that takes care of setting up all the dependencies to build and push a Docker image.

## inputs

| Name               | Required | Description                |
| ------------------ | -------- | -------------------------- |
| imageName          | `true`   | Image name to push         |
| target             | `false`  | Docker target to build     |
| context            | `true`   | Docker context to use      |
| dockerfilePath     | `false`  | Dockerfile path            |
| commit             | `true`   | Commit SHA                 |
| registryBaseUrl    | `true`   | Docker registry base URL   |
| registryRepository | `true`   | Registry repository to use |
| registryUsername   | `true`   | Docker registry user       |
| registryPassword   | `true`   | Docker registry password   |

## usage

To build and push a service image, make sure to check out the codebase beforehand, then invoke the action and pass all necessary inputs.

```yaml
name: Build images
on:
  workflow_dispatch:
  push:
    branches:
      - main
jobs:
  build-images:
    name: Build service image
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      # uses latest version of the action
      - uses: brunoscheufler/docker-build-push@main
        with:
          imageName: my-service
          context: .
          commit: ${{ github.sha }}
          registryBaseUrl: ghcr.io
          registryRepository: my-repo
          registryUsername: my-org
          registryPassword: ${{ secrets.GITHUB_TOKEN }}
```
