# Build SSH Connection Action

This GitHub Action simplifies establishing an SSH connection by preparing an SSH chain to a remote server. It handles generating an SSH key, setting permissions, and adding the server to the `known_hosts` file, ensuring a seamless and secure connection process.

## Features

- Automatically generates and stores SSH keys.
- Adds the remote server to the `~/.ssh/known_hosts` file.
- Constructs an SSH chain with specified user and port.

## Inputs

| Name             | Description              | Required | Default |
|------------------|--------------------------|----------|---------|
| `remote-host`    | Remote host address      | Yes      |         |
| `remote-port`    | Remote port (optional)   | No       | 22      |
| `remote-user`    | Remote username          | Yes      |         |
| `remote-ssh-key` | Remote SSH private key   | Yes      |         |

## Outputs

| Name               | Description                        |
|--------------------|------------------------------------|
| `remote-server`    | The remote server's address        |
| `remote-ssh-chain` | SSH chain to the remote server     |


## How It Works

1. The action generates an SSH key and stores it in ~/.ssh/id_rsa.
2. Adds the remote server to the ~/.ssh/known_hosts file using `ssh-keyscan`.
3. Constructs the SSH chain string (user@host:port) for use in subsequent steps.
 
## Usage

Below is an example of how to use this action in your workflow:

```
jobs:
  build-ssh:
    runs-on: ubuntu-latest
    steps:
      - name: Build SSH Connection
        uses: ./
        with:
          remote-host: example.com
          remote-port: 2222
          remote-user: ubuntu
          remote-ssh-key: ${{ secrets.SSH_PRIVATE_KEY }}
```
