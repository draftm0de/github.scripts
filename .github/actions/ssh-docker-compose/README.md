# SSH Docker Compose Action

This GitHub Action simplifies executing Docker Compose commands on a remote server over SSH. It supports optional Docker login for private repositories and streamlines container management workflows.

## Features

- Runs Docker Compose commands on a remote server.
- Optionally logs in to Docker for accessing private repositories.
- Handles secure SSH-based remote execution.

## Inputs

| Name               | Description                                      | Required | Default |
|--------------------|--------------------------------------------------|----------|---------|
| `command`          | Docker Compose command to execute                | Yes      |         |
| `remote-ssh-chain` | SSH chain to the remote server (user@host:port)  | Yes      |         |
| `remote-path`      | Root directory path on the remote server         | Yes      |         |
| `docker-registry`  | To be used docker registry (default: Docker hub) | No       |         |
| `docker-username`  | Docker registry username for authentication      | No       |         |
| `docker-token`     | Docker registry token for authentication         | No       |         |

## How It Works

1. Optionally performs a Docker login if credentials are provided.
2. Executes the specified Docker Compose command on the remote server.
3. Uses SSH to securely connect and manage remote server operations.

## Usage

Below is an example of how to use this action in your workflow:

```
jobs:
  run-docker-compose:
    runs-on: ubuntu-latest
    steps:
      - name: Run Docker Compose
        uses: ./.github/actions/ssh-docker-compose@main
        with:
          command: up -d
          remote-ssh-chain: ${{ secrets.SSH_CHAIN }}
          remote-path: /remote/docker/path
          docker-username: ${{ secrets.DOCKER_USERNAME }}
          docker-token: ${{ secrets.DOCKER_TOKEN }}
```
using `ghcr.io` as registry
```
jobs:
  run-docker-compose:
    runs-on: ubuntu-latest
    steps:
      - name: Run Docker Compose
        uses: ./.github/actions/ssh-docker-compose@main
        with:
          command: up -d
          remote-ssh-chain: ${{ secrets.SSH_CHAIN }}
          remote-path: /remote/docker/path
          docker-registry: ghcr.io          
          docker-username: ${{ secrets.DOCKER_USERNAME }}
          docker-token: ${{ secrets.DOCKER_TOKEN }}
```
