# Deploy App to S3 Bucket GitHub Action

## Description

The "Deploy App to S3" GitHub Action automates the process of uploading a build app to an AWS S3 bucket. This action is particularly useful for hosting static web applications on S3. It uploads the build artifacts, excluding the `index.html` file, and then uploads the `index.html` file separately with a different cache control value.

## Inputs

1. `aws-region` (required, type: string): The AWS Region where the S3 bucket is located.

2. `aws-s3-bucket` (required, type: string): The name of the AWS S3 bucket where the build app will be deployed.

3. `destination` (optional, type: string): The directory inside the S3 bucket where the build artifacts will be uploaded. The default value is "build".

## Workflow Example

```yaml
name: Deploy App to S3

on:
  push:
    branches:
      - main

jobs:
  deploy-to-s3:
    runs-on: ubuntu-latest
    name: Deploy App to S3 Bucket
    steps:
      # Step 1: Checkout the repository
      - name: Checkout
        uses: actions/checkout@v3

      # Step 2: Run the Deploy App to S3 action
      - name: Deploy App to S3
        id: deploy-to-s3
        uses: ingeno/foundation-github-actions/actions/deploy-app-to-s3-action@v3
        with:
          aws-region: ca-central-1
          aws-s3-bucket: my-s3-bucket
          destination: my-build-directory

      # Step 3: Optionally use the outputs in subsequent steps (example)
      - name: Display Deployment Details
        shell: bash
        run: |
          echo "AWS Region: ${{ inputs.aws-region }}"
          echo "S3 Bucket: ${{ inputs.aws-s3-bucket }}"
          echo "Destination Directory: ${{ inputs.destination }}"
```

## Notes

- Before using this action, ensure that you have set up the necessary AWS credentials to authenticate with the AWS S3 (e.g. by using the `configure-aws-credentials` action).