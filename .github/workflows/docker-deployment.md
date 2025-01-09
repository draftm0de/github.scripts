# Docker Compose Deployment Workflow

This reusable GitHub Actions workflow automates deploying applications using Docker Compose on a remote server. It handles file synchronization, SSH connections, Docker authentication, and Docker Compose commands.

## Features

- Establishes an SSH connection to the remote server using a secure key.
- Synchronizes deployment files to the remote server.
- Optionally authenticates with Docker for private repository access.
- Executes Docker Compose commands to deploy or update the application.

## Inputs

| Name              | Description                                 | Required | Default |
|-------------------|---------------------------------------------|----------|---------|
| `remote-host`     | Remote server hostname or IP address        | Yes      |         |
| `remote-port`     | Remote SSH port                             | No       | `22`    |
| `remote-user`     | Remote SSH username                         | Yes      |         |
| `remote-path`     | Root directory path on the remote server    | Yes      |         |
| `transfer-files`  | Comma-separated list of files to transfer   | Yes      |         |
| `docker-registry` | Docker registry (default: Docker hub)       | No       |         |
| `docker-command`  | To be executed docker compose command       | No       |         |
| `docker-username` | Docker registry username for authentication | No       |         |

## Secrets

| Name             | Description                        | Required |
|------------------|------------------------------------|----------|
| `DOCKER_TOKEN`   | Docker login token                 | No       |
| `REMOTE_SSH_KEY` | SSH private key for authentication | Yes      |

## How It Works

1. **SSH Connection:**
- Establishes a secure SSH connection to the remote server using the provided credentials and private key. 
2. **File Synchronization:**
- Transfers the specified deployment files (e.g., docker-compose.yml, .env) to the remote server.
3. **Docker Authentication:**
- Optionally logs in to Docker on the remote server using the provided credentials and token.
4. **Docker Compose Execution:**
- Runs the specified Docker Compose command (e.g. up -d) to deploy or update the application on the remote server.
- The argument `docker-command` is optional and will be only executed if provided

## Usage Example

```
name: Docker Compose Deployment Example

on:
  push:
    branches:
      - main

jobs:
  deploy:
    uses: ./.github/workflows/docker-deployment.yml
    with:
      remote-host: example.com
      remote-user: deploy
      remote-path: /var/www/app
      transfer-files: docker-compose.yml,.env
      docker-command: up -d
      docker-username: mydockerusername
    secrets:
      REMOTE_SSH_KEY: ${{ secrets.REMOTE_SSH_KEY }}
      DOCKER_TOKEN: ${{ secrets.DOCKER_TOKEN }}
```