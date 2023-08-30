# AWS Docker Deploy GitHub Workflow

## Description

The AWS Docker Deploy GitHub Action automates the process of building, tagging, and pushing a Docker image to Amazon Elastic Container Registry (ECR). This action is particularly useful when deploying containerized applications to AWS using GitHub Actions.

## Usage

To use this GitHub Action, you need to define it in your workflow file (e.g., `.github/workflows/aws_docker_deploy.yml`) and set up the required inputs. Below are the inputs supported by this action:

### Inputs

1. `repository` (required, type: string): The name of the repository where the Docker image will be pushed to ECR.

2. `dockerfile` (required, type: string): The location of the Dockerfile used to build the Docker image.

3. `client-environment-file-path` (optional, type: string): The location of the `.env` file for the front-end client, if applicable. This file is used to configure environment variables for the client application.

4. `dotenv-value` (optional, type: string): The value needed to fill the `.env` file for the front-end client. This input is only relevant if `client-environment-file-path` is provided.

5. `npm-read-packages-token` (optional, type: string): Token for reading NPM packages from private repositories

### Permissions

For this action to work properly, the following permissions are needed to interact with GitHub's OIDC Token endpoint:

- `id-token`: write
- `contents`: read

## Usage Example

```yaml
jobs:
  build-backend-api:
    name: Build backend-api
    uses: ingeno/foundation-github-actions/workflows/aws-docker-deploy.yml@v3
    secrets: inherit
    with:
      repository: your-repository-name
      dockerfile: your/dockerfile/path/Dockerfile
```

## Notes

- This action assumes that you have already set up the necessary AWS credentials and permissions to interact with the ECR repository.
- Ensure that the required environment variables, if any, are properly set to configure the AWS CLI and access ECR.
