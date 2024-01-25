# AWS Docker Deploy GitHub Workflow

## Description

The AWS Docker Deploy GitHub Action automates the process of building, tagging, and pushing a Docker image to Amazon Elastic Container Registry (ECR). This action is particularly useful when deploying containerized applications to AWS using GitHub Actions.

## Usage

To use this GitHub Action, you need to define it in your workflow file (e.g., `.github/workflows/aws_docker_deploy.yml`) and set up the required inputs. Below are the inputs supported by this action:

### Inputs

1. `repository` (required, type: string): The name of the repository where the Docker image will be pushed to ECR.

2. `dockerfile` (required, type: string): The location of the Dockerfile used to build the Docker image.

3. `environment-file-path` (optional, type: string): The location of the `.env` file for the app, if applicable. This file is used to configure environment variables when required by the process used for building and deploying. See details for each parts of the application to determine if needed, for example for Next.js deployments.

4. `dotenv-value` (optional, type: string): The value needed to fill the `.env` file. This input is only relevant if `environment-file-path` is provided.

5. `working-directory` (optional, type: string): The current working directory to run the docker command in. If not provided, the default value is `./`.

### Secrets

1. `NPM_READ_PACKAGES_TOKEN` (optional, type: string): Token for reading NPM packages from private repositories

### Permissions

For this action to work properly, the following permissions are needed to interact with GitHub's OIDC Token endpoint:

- `id-token`: write
- `contents`: read

## Usage Example

```yaml
jobs:
  build-backend-api:
    name: Build backend-api
    uses: ingeno/foundation-github-actions/workflows/global--aws-docker-deploy.yml@v3
    secrets: inherit
    with:
      repository: your-repository-name
      dockerfile: your/dockerfile/path/Dockerfile
```

## Notes

- This action assumes that you have already set up the necessary AWS credentials and permissions to interact with the ECR repository.
- Ensure that the required environment variables, if any, are properly set to configure the AWS CLI and access ECR.
