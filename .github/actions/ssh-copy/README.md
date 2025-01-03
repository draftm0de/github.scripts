# SSH Copy Files Action

This GitHub Action facilitates secure file transfers to a remote server over SSH. It handles creating remote directories and copying files, ensuring efficient and reliable file synchronization.

## Features

- Copies files to a remote server via SSH.
- Automatically creates directories on the remote server if they don't exist.
- Supports specifying custom source and target paths for file transfers.

## Inputs

| Name               | Description                          | Required | Default |
|--------------------|--------------------------------------|----------|---------|
| `files`            | Files to be transferred, separated by commas. Can specify custom target paths using `:` (e.g., `source:file`) | Yes      |         |
| `remote_ssh_chain` | SSH chain to the remote server (user@host:port) | Yes      |         |
| `remote_path`      | Root directory path on the remote server | Yes      |         |

## Usage

Below is an example of how to use this action in your workflow:

```
jobs:
  copy-files:
    runs-on: ubuntu-latest
    steps:
      - name: Copy Files via SSH
        uses: ./
        with:
          files: file1.txt,file2.txt:/remote/target/path/file2.txt
          remote_ssh_chain: ${{ secrets.SSH_CHAIN }}
          remote_path: /remote/root/path
```

## How It Works

1. Splits the list of files provided as input into individual entries.
2. For each file:
   - Creates the target directory on the remote server if it doesn't exist.
   - Transfers the file using `scp`.
   - Skips optional files that don't exist locally, but fails the process for required files (indicated with a `+` prefix).
3. Logs the process and errors, ensuring transparency.