# Push Docker Image Action

This GitHub Action allows you to push Docker images to a registry. It supports loading images from artifacts, tagging them with new names, and securely authenticating with Docker Hub.

## Features

- Pushes Docker images directly or loads them from artifacts.
- Supports tagging images with new target names before pushing.
- Authenticates securely using a Docker API token.

## Inputs

| Name                  | Description                          | Required | Default |
|-----------------------|--------------------------------------|----------|---------|
| `image`               | Docker image name to push            | No       |         |
| `artifact`            | Load the image from an artifact      | No       |         |
| `target`              | Target Docker image name for tagging | No       |         |
| `secret-docker-token` | Docker API token for authentication  | Yes      |         |

## How It Works

1. **Load Docker Image**:
    - If the `artifact` input is provided, the action downloads and loads the image from the specified artifact.
    - If the `image` input is provided, it uses the specified Docker image directly.

2. **Prepare Push Arguments**:
    - Verifies the provided image or artifact is valid and accessible.
    - Extracts the Docker username from the image name.

3. **Login to Docker Hub**:
    - Logs into Docker Hub using the provided username and API token.

4. **Push Docker Image**:
    - Optionally tags the image with the name provided in the `target` input.
    - Pushes the image to the Docker registry.

## Usage Example

```yaml
jobs:
  push-docker-image:
    runs-on: ubuntu-latest
    steps:
      - name: Push Docker Image
        uses: ./
        with:
          image: myrepo/myimage:1.0
          secret-docker-token: ${{ secrets.DOCKER_TOKEN }}
          target: myrepo/myimage:latest
```