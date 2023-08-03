# Docker Deploy GitHub Action

## Description

The "Docker Deploy" GitHub Action automates the process of building, tagging, and pushing a Docker image to a container registry. This action simplifies the deployment of containerized applications and makes it easy to publish new versions of your Docker images.

## Inputs

1. `registry` (required, type: string): The URL of the container image registry where the Docker image will be pushed.

2. `repository` (required, type: string): The name of the repository for the Docker image.

3. `tag` (optional, type: string): The tag of the built image. If not provided, the default value is "dev".

4. `dockerfile` (optional, type: string): The location of the Dockerfile used to build the Docker image. If not provided, the default value is "Dockerfile".

## Workflow Example

```yaml
name: Docker Deploy

on:
  push:
    branches:
      - main

jobs:
  docker-deploy:
    runs-on: ubuntu-latest
    name: Docker Build, Tag, and Push
    steps:
      # Step 1: Checkout the repository
      - name: Checkout
        uses: actions/checkout@v3

      # Step 2: Run the Docker Deploy action
      - name: Docker Deploy
        id: docker-deploy
        uses: ingeno/foundation-github-actions/actions/docker-deploy@<latest>
        with:
          registry: your-container-registry.example.com
          repository: my-docker-repo
          tag: v1.0.1
          dockerfile: path/to/Dockerfile

      # Step 3: Optionally use the outputs in subsequent steps (example)
      - name: Display Docker Image Details
        shell: bash
        run: |
          echo "Registry: ${{ inputs.registry }}"
          echo "Repository: ${{ inputs.repository }}"
          echo "Tag: ${{ inputs.tag }}"
          echo "Dockerfile: ${{ inputs.dockerfile }}"
```

## Notes

- Before using this action, ensure that you have set up the necessary credentials to authenticate with the container image registry by setting the `SHARED_SERVICES_ACCOUNT_ID` variable in your repository.
- To see what the current latest version of this action is, head over to this repository's [release page](https://github.com/ingeno/foundation-github-actions/releases).