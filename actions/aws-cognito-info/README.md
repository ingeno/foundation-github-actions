# AWS Cognito Information GitHub Action

## Description

The "AWS Cognito Information" GitHub Action retrieves important information related to an AWS Cognito user pool and its client ID in the specified AWS Region. This action uses the AWS CLI to query the Cognito service and obtain the required details.

## Inputs

1. `aws-region` (required, type: string): The AWS Region where the Cognito user pool is located.

## Outputs

This action provides the following outputs that can be used in subsequent steps or workflows:

1. `user-pool-id`: The AWS Cognito user pool ID.

2. `user-pool-client-id`: The AWS Cognito user pool client ID.

## Usage Example

```yaml
name: Get AWS Cognito Information

on:
  push:
    branches:
      - main

jobs:
  get-cognito-info:
    runs-on: ubuntu-latest
    name: Get AWS Cognito Information
    steps:
      # Step 1: Checkout the repository
      - name: Checkout
        uses: actions/checkout@v3

      # Step 2: Run the AWS Cognito Information action
      - name: Get AWS Cognito Information
        id: cognito-info
        uses: ingeno/foundation-github-actions/actions/aws-cognito-information-action@v2
        with:
          aws-region: ca-central-1

      # Step 3: Use the outputs in subsequent steps (example)
      - name: Display AWS Cognito Information
        shell: bash
        run: |
          echo "AWS Cognito Information:"
          echo "User Pool ID: ${{ steps.cognito-info.outputs.user-pool-id }}"
          echo "User Pool Client ID: ${{ steps.cognito-info.outputs.user-pool-client-id }}"
```

## Notes

- Before using this action, ensure that you have set up the necessary AWS credentials to access AWS Cognito (e.g. by using the `configure-aws-credentials` action).