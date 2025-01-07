# SSH Docker Login Action

This GitHub Action facilitates secure Docker login on a remote server over SSH, enabling seamless access to private Docker repositories. It handles the creation and secure transfer of authentication tokens.

## Features

- Securely logs in to Docker on a remote server using SSH.
- Transfers Docker authentication tokens securely.
- Cleans up authentication tokens after use for enhanced security.

## Inputs

| Name               | Description                                     | Required | Default |
|--------------------|-------------------------------------------------|----------|---------|
| `remote-ssh-chain` | SSH chain to the remote server (user@host:port) | Yes      |         |
| `remote-path`      | Root directory path on the remote server        | Yes      |         |
| `docker-username`  | Docker registry username                        | Yes      |         |
| `docker-token`     | Docker registry token                           | Yes      |         |
| `docker-registry`  | Docker registry (default: Docker hub)           | No       |         |

## How It Works

1. Generates a local token file and transfers it to the remote server.
2. Logs in to Docker on the remote server using the provided credentials.
3. Removes the token file from both local and remote locations to ensure security.

## Usage

Below is an example of how to use this action in your workflow:

```
jobs:
  docker-login:
    runs-on: ubuntu-latest
    steps:
      - name: Perform Docker Login on Remote
        uses: ./.github/actions/ssh-docker-login@main
        with:
          remote-ssh-chain: ${{ secrets.SSH_CHAIN }}
          remote-path: /remote/docker/path
          docker-username: ${{ secrets.DOCKER_USERNAME }}
          docker-token: ${{ secrets.DOCKER_TOKEN }}
```
using `ghcr.io` as registry
```
jobs:
  docker-login:
    runs-on: ubuntu-latest
    steps:
      - name: Perform Docker Login on Remote
        uses: ./.github/actions/ssh-docker-login@main
        with:
          remote-ssh-chain: ${{ secrets.SSH_CHAIN }}
          remote-path: /remote/docker/path
          docker-registry: ghcr.io
          docker-username: ${{ secrets.DOCKER_USERNAME }}
          docker-token: ${{ secrets.DOCKER_TOKEN }}
```
