# Configure AWS Credentials GitHub Action

## Description

The "Configure AWS Credentials" GitHub Action sets up AWS credentials for GitHub OIDC (OpenID Connect) to interact with AWS services using the specified AWS account and region. This action assumes the presence of a role named "AWSGitHubActionRoleForCICD," which is defined by the `@ingeno/aws-cdk-constructs` library.

## Inputs

1. `aws-account-id` (required, type: string): The AWS Account ID where the role "AWSGitHubActionRoleForCICD" is defined.

2. `aws-region` (required, type: string): The AWS Region where the AWS services will be accessed.

## Workflow Example

```yaml
name: Configure AWS Credentials

on:
  push:
    branches:
      - main

jobs:
  configure-aws-credentials:
    runs-on: ubuntu-latest
    name: Configure AWS Credentials for GitHub OIDC
    steps:
      # Step 1: Checkout the repository
      - name: Checkout
        uses: actions/checkout@v3

      # Step 2: Run the Configure AWS Credentials action
      - name: Configure AWS Credentials
        id: configure-aws-credentials
        uses: ingeno/foundation-github-actions/actions/configure-aws-credentials-action@v3
        with:
          aws-account-id: 123456789012
          aws-region: ca-central-1

      # Step 3: Optionally use the outputs in subsequent steps (example)
      - name: Display AWS Credentials Configuration
        shell: bash
        run: |
          echo "AWS Account ID: ${{ inputs.aws-account-id }}"
          echo "AWS Region: ${{ inputs.aws-region }}"
```

## Notes

- Before using this action, ensure that you have set up the necessary AWS credentials with sufficient permissions to assume the role "AWSGitHubActionRoleForCICD."
- The action uses the `aws-actions/configure-aws-credentials@v2` action to set up the AWS credentials for OIDC.