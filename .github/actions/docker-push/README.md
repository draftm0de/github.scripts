# Push Docker Image Action

This GitHub Action allows you to push Docker images to a registry. It supports loading images from artifacts, tagging them with new names, and securely authenticating with Docker Hub.

## Features

- Pushes Docker images directly or loads them from artifacts.
- Supports tagging images with new target names before pushing.
- Authenticates securely using a Docker API token.

## Inputs

| Name                  | Description                                 | Required | Default |
|-----------------------|---------------------------------------------|----------|---------|
| `image`               | Docker image name to push                   | No       |         |
| `artifact`            | Load the image from an artifact             | No       |         |
| `target`              | Target Docker image name for tagging        | No       |         |
| `docker-username`     | Docker registry username for authentication | No       |         |
| `docker-registry`     | Docker registry (default: Docker hub)       | No       |         |
| `secret-docker-token` | Docker API token for authentication         | Yes      |         |

## How It Works

1. **Load Docker Image**:
   - If the `artifact` input is provided, the action downloads and loads the image from the specified artifact.
   - If the `image` input is provided, it uses the specified Docker image directly.

2. **Prepare Push Arguments**:
   - Verifies the provided image or artifact is valid and accessible.
   - Extracts the Docker username from the image name.

3. **Login to Docker Registry**:
   - Logs into Docker registry using the provided username and API token.

4. **Push Docker Image**:
    - Optionally tags the image with the name provided in the `target` input.
    - Pushes the image to the Docker registry.

## Registries
### registry: ghcr.io 
#### Enable `GITHUB_TOKEN` for Organization Repositories
For workflows in an organization repository, you may need to explicitly enable the GITHUB_TOKEN for package publishing:
1. Go to your repository's **Settings → Actions → General**.
2. Under the **Workflow permissions** section:
   - Select **Read and write permissions**.
   - Enable **Allow GitHub Actions to create and approve pull requests** if necessary.
#### Update Workflow Permissions
By default, the GITHUB_TOKEN provided by GitHub Actions has limited permissions. You need to explicitly grant it permissions to packages in your workflow.

Add the following under your workflow’s top-level permissions key:
```
permissions:
  contents: write
  packages: write
```

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

using `ghci.io` as docker registry.
```yaml
permissions:
   contents: write
   packages: write
   
jobs:
  push-docker-image:
    runs-on: ubuntu-latest
    steps:
      - name: Push Docker Image
        uses: ./
        with:
          image: myrepo/myimage:1.0
          docker-registry: ghci.io
          secret-docker-token: ${{ secrets.GITHUB_TOKEN }}
          target: myrepo/myimage:latest
```