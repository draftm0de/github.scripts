# Draftmode´s Github Scripts

Welcome to the documentation for the suite of GitHub Actions designed to streamline Docker workflows and remote server operations. These actions are built to provide flexibility, security, and efficiency for developers managing Docker images, SSH connections, and artifact-based workflows.

Each action addresses a specific need within the DevOps lifecycle, from building and pushing Docker images to managing SSH-based interactions and artifact handling. With these tools, you can automate and optimize your CI/CD pipelines, ensuring consistent and reliable deployments.

The following sections detail each action, their features, inputs, outputs, and how they work. Explore the capabilities of these actions and integrate them into your workflows to enhance productivity and simplify complex tasks.

## Action Scripts

| Action                                                               | Summary                                                                                                   |
|----------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------|
| [artifact-from-image](.github/actions/artifact-from-image/README.md) | save Docker images as artifacts for easy storage and reuse across workflows.                              |
| [artifact-to-image](.github/actions/artifact-to-image/README.md)     | load Docker images from artifacts for reuse in workflows.                                                 |
| [docker-build](.github/actions/docker-build/README.md)               | building Docker images with advanced options and reproducibility, and uploading the results as artifacts. |
| [docker-push](.github/actions/docker-push/README.md)                 | push Docker images, supporting artifact-based loading, tagging, and secure Docker Hub authentication.     |
| [ssh-connect](.github/actions/ssh-connect/README.md)                 | automate building secure SSH connections to remote servers.                                               |
| [ssh-copy](.github/actions/ssh-copy/README.md)                       | securely transfer files to remote servers with automated directory creation and flexible file mapping.    |
| [ssh-docker-compose](.github/actions/ssh-docker-compose/README.md)   | executing Docker Compose commands on remote servers, with optional Docker authentication.                 |
| [ssh-docker-login](.github/actions/ssh-docker-login/README.md)       | securely log in to Docker on remote servers via SSH, enabling access to private repositories.             |

## Workflows