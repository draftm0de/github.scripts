# SSH Docker Login Action

This GitHub Action facilitates secure Docker login on a remote server over SSH, enabling seamless access to private Docker repositories. It handles the creation and secure transfer of authentication tokens.

## Features

- Securely logs in to Docker on a remote server using SSH.
- Transfers Docker authentication tokens securely.
- Cleans up authentication tokens after use for enhanced security.

## Inputs

| Name               | Description                                     | Required | Default |
|--------------------|-------------------------------------------------|----------|---------|
| `remote_ssh_chain` | SSH chain to the remote server (user@host:port) | Yes      |         |
| `remote_path`      | Root directory path on the remote server        | Yes      |         |
| `docker_username`  | Docker Hub username                             | Yes      |         |
| `docker_token`     | Docker Hub token                                | Yes      |         |

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
        uses: ./
        with:
          remote_ssh_chain: ${{ secrets.SSH_CHAIN }}
          remote_path: /remote/docker/path
          docker_username: ${{ secrets.DOCKER_USERNAME }}
          docker_token: ${{ secrets.DOCKER_TOKEN }}
```
