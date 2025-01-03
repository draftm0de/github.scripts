# Build Docker Image Action

This GitHub Action builds Docker images from a specified context, supports advanced options like build targets and reproducible images, and uploads the built image as an artifact.

## Features

- Builds Docker images with support for `--target` and additional build options.
- Enables reproducible builds with `docker buildx`.
- Reads build arguments from a file for advanced configurations.
- Uploads the built image as an artifact for storage and reuse.

## Inputs

| Name              | Description                                             | Required | Default |
|-------------------|---------------------------------------------------------|----------|---------|
| `image`           | Docker image name (e.g., `repo/image:tag`)              | Yes      |         |
| `target`          | Build `--target` option                                 | No       |         |
| `context`         | Build context (e.g., directory to build)                | No       | `.`     |
| `reproducible`    | Enable reproducible builds (true/false)                 | No       |         |
| `options`         | Additional build options                                | No       |         |
| `build_args_file` | File containing build arguments (`--build-arg`)         | No       |         |

## Outputs

| Name       | Description                                |
|------------|--------------------------------------------|
| `digest`   | Digest of the built Docker image           |
| `artifact` | Name of the uploaded Docker image artifact |


## How It Works

1. **Prepare Build Arguments:**
   - Parses the provided inputs to construct Docker build arguments and options.
   - Reads additional build arguments from a file, if specified.
   - Determines the image name, tag, and build context.
2. **Set Up for Reproducible Builds:**
   - If reproducible is enabled, sets up docker buildx for deterministic builds.
3. **Build Docker Image:**
   - Executes the build using docker build or docker buildx build depending on the reproducibility setting.
   - Extracts the image digest after a successful build.
4. **Upload the Built Image:**
   - Uploads the built Docker image as an artifact using a specified action.
 
## Usage Example

```
jobs:
  build-docker-image:
    runs-on: ubuntu-latest
    steps:
      - name: Build Docker Image
        uses: ./
        with:
          image: myrepo/myimage:1.0
          context: ./docker
          reproducible: true
          options: --no-cache
          build_args_file: build-args.txt
```
