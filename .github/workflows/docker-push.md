# Docker Push Image Workflow

This reusable GitHub Actions workflow streamlines the process of pushing Docker images to a registry. It supports pushing images directly or from artifacts and allows tagging images with a target name.

## Features

- Pushes Docker images directly or loads them from artifacts.
- Optionally tags images with a new target name before pushing.
- Uses a secure Docker token for authentication.

## Inputs

| Name              | Description                                        | Required | Default |
|-------------------|----------------------------------------------------|----------|---------|
| `image`           | Source Docker image name to push                   | No       |         |
| `artifact`        | Artifact name to load the Docker source image from | No       |         |
| `target`          | Target Docker image name for tagging               | No       |         |
| `docker-username` | Docker registry username for authentication        | No       |         |
| `docker-registry` | Docker registry (default: Docker hub)              | No       |         |

## Secrets

| Name           | Description                         | Required |
|----------------|-------------------------------------|----------|
| `DOCKER_TOKEN` | Docker API token for authentication | Yes      |

## How It Works

1. **Prepare Push Arguments:**
- Verifies whether the image will be pushed directly or loaded from an artifact.
- Ensures that at least one input (image or artifact) is provided.
2. **Push Docker Image:**
- Loads the Docker image from the specified artifact or uses the given image. 
- Optionally tags the image with the target name before pushing. 
- Authenticates with Docker Hub using the provided token and pushes the image.

## Usage Example

```
name: Push Docker Image Example

on:
  push:
    branches:
      - main

jobs:
  push-docker-image:
    uses: ./.github/workflows/docker-push.yml
    with:
      image: myrepo/myimage:1.0
      target: myrepo/myimage:latest
    secrets:
      DOCKER_TOKEN: ${{ secrets.DOCKER_TOKEN }}
      
  push-docker-image-ghci-io:
    uses: ./.github/workflows/docker-push.yml
    with:
      image: myrepo/myimage:1.0
      target: myrepo/myimage:latest
      docker-registry: ghci.io
    secrets:
      DOCKER_TOKEN: ${{ secrets.DOCKER_TOKEN }}
```