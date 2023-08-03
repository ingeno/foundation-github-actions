# Tag Docker Image GitHub Action

## Description

The "Tag Docker Image" GitHub Action allows you to tag an existing Docker image in the AWS Elastic Container Registry (ECR). This action helps you apply new tags to an existing image, which can be useful for versioning and tracking changes.

## Inputs

1. `repository` (required, type: string): The name of the git repository in the AWS ECR where the image is located.

2. `sourceTag` (optional, type: string): The tag of the source image. If provided, the action will use this tag to find the existing image in the repository. If not provided, the action will assume that the target tag is being applied to an image that already exists in the repository.

3. `targetTag` (required, type: string): The tag to be applied to the existing Docker image. This will create a new reference to the same image with the specified tag.

## Workflow Example

```yaml
name: Tag Docker Image

on:
  push:
    branches:
      - main

jobs:
  tag-docker-image:
    runs-on: ubuntu-latest
    name: Tag Docker Image
    steps:
      # Step 1: Checkout the repository
      - name: Checkout
        uses: actions/checkout@v3

      # Step 2: Run the Tag Docker Image action
      - name: Tag Docker Image
        id: tag-docker-image
        uses: ingeno/foundation-github-actions/actions/aws-docker-tag@<latest>
        with:
          repository: my-ecr-repo
          sourceTag: latest
          targetTag: v1.0.1

      # Step 3: Optionally use the outputs in subsequent steps (example)
      - name: Display Docker Image Tags
        shell: bash
        run: |
          echo "Docker Image Tags:"
          echo "Source Tag: ${{ inputs.sourceTag }}"
          echo "Target Tag: ${{ inputs.targetTag }}"
```

## Notes

- Before using this action, ensure that you have set up the necessary AWS credentials to authenticate with the AWS ECR (e.g. by using the `configure-aws-credentials` action).
- To see what the current latest version of this action is, head over to this repository's [release page](https://github.com/ingeno/foundation-github-actions/releases).