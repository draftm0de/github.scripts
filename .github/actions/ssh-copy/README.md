# SSH Copy Files Action

This GitHub Action facilitates secure file transfers to a remote server over SSH. It handles creating remote directories and copying files, ensuring efficient and reliable file synchronization.

### Required
For copy/sync directories the action is using `rsync`. The remote server has to have this package installed.
- for Debian
```
apt update && apt install rsync
```

## Features

- Copies files to a remote server via SSH.
- Automatically creates directories on the remote server if they don't exist.
- Supports specifying custom source and target paths for file transfers.

## Inputs

| Name               | Description                                                                                                               | Required | Default |
|--------------------|---------------------------------------------------------------------------------------------------------------------------|----------|---------|
| `files`            | Files/directories to be transferred, separated by commas. Can specify custom target paths using `:` (e.g., `source:file`) | Yes      |         |
| `remote-ssh-chain` | SSH chain to the remote server (user@host:port)                                                                           | Yes      |         |
| `remote-path`      | Root directory path on the remote server                                                                                  | Yes      |         |

## How It Works

1. Splits the list of files/directories provided as input into individual entries.
2. For each file/directory:
   - Creates the target directory on the remote server if it doesn't exist.
   - Transfers the file using `scp` or via `rsync -avz --delete -e` in case of a directory.
   - Skips optional files that don't exist locally, but fails the process for required files (indicated with a `+` prefix).
3. Logs the process and errors, ensuring transparency.

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
          remote-ssh-chain: ${{ secrets.SSH_CHAIN }}
          remote-path: /remote/root/path
```
