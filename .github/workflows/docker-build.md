# Docker Build Image Workflow

This reusable GitHub Actions workflow facilitates building Docker images with flexibility and advanced configuration options. It supports build arguments, reproducible builds, and outputs artifacts for further use in workflows.

## Features

- Supports advanced Docker build configurations such as `--target` and additional build options.
- Reads build arguments from a file for dynamic and reusable builds.
- Provides reproducible builds for consistency across environments.
- Outputs the built image artifact name and digest for downstream workflows.

## Inputs

| Name              | Description                                             | Required | Default |
|-------------------|---------------------------------------------------------|----------|---------|
| `image`           | Docker image name (e.g., `repo/image:tag`)              | Yes      |         |
| `target`          | Build `--target` option                                 | No       |         |
| `context`         | Build context (e.g., directory to build)                | No       | `.`     |
| `options`         | Additional build options                                | No       |         |
| `build-args-file` | File containing build arguments (`--build-arg`)         | No       |         |
| `reproducible`    | Enable reproducible builds (true/false)                 | No       |         |

## Outputs

| Name       | Description                             |
|------------|-----------------------------------------|
| `artifact` | Name of the built Docker image artifact |
| `digest`   | Digest of the built Docker image        |

## Usage Example

```
name: Build Docker Image Example

on:
  push:
    branches:
      - main

jobs:
  build-docker-image:
    uses: ./.github/workflows/docker-build.yml
    with:
      image: myrepo/myimage:1.0
      context: ./docker
      options: --no-cache
      build-args-file: build-args.txt
      reproducible: true
```