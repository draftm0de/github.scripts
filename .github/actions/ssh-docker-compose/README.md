# SSH Docker Compose Action

This GitHub Action simplifies executing Docker Compose commands on a remote server over SSH. It supports optional Docker login for private repositories and streamlines container management workflows.

## Features

- Runs Docker Compose commands on a remote server.
- Optionally logs in to Docker for accessing private repositories.
- Handles secure SSH-based remote execution.

## Inputs

| Name               | Description                               | Required | Default |
|--------------------|-------------------------------------------|----------|---------|
| `command`          | Docker Compose command to execute         | Yes      |         |
| `remote_ssh_chain` | SSH chain to the remote server (user@host:port) | Yes      |         |
| `remote_path`      | Root directory path on the remote server  | Yes      |         |
| `docker_username`  | Docker Hub username for authentication    | No       |         |
| `docker_token`     | Docker Hub token for authentication       | No       |         |

## Usage

Below is an example of how to use this action in your workflow:

```
jobs:
  run-docker-compose:
    runs-on: ubuntu-latest
    steps:
      - name: Run Docker Compose
        uses: ./
        with:
          command: up -d
          remote_ssh_chain: ${{ secrets.SSH_CHAIN }}
          remote_path: /remote/docker/path
          docker_username: ${{ secrets.DOCKER_USERNAME }}
          docker_token: ${{ secrets.DOCKER_TOKEN }}
```

## How It Works

1. Optionally performs a Docker login if credentials are provided.
2. Executes the specified Docker Compose command on the remote server.
3. Uses SSH to securely connect and manage remote server operations.