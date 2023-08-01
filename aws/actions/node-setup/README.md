# Node Setup GitHub Action

## Description

The "Node Setup" GitHub Action automates the setup of Node.js environment by reading the `.nvmrc` file, using `nvm` to select the specified Node.js version, and installing project dependencies using Yarn. The action also caches the Yarn cache directory to speed up the installation process for subsequent runs.

## Inputs

1. `working-directory` (optional, type: string): The current working directory to set up Node.js into. The default value is `'.'`.

## Workflow Example

```yaml
name: Node Setup

on:
  push:
    branches:
      - main

jobs:
  node-setup:
    runs-on: ubuntu-latest
    name: Node Setup
    steps:
      # Step 1: Checkout the repository
      - name: Checkout
        uses: actions/checkout@v3

      # Step 2: Run the Node Setup action
      - name: Node Setup
        id: node-setup
        uses: ingeno/foundation-github-actions/aws/actions/node-setup/node-setup-action@v3
        with:
          working-directory: my-project-directory

      # Step 3: Optionally use the outputs in subsequent steps (example)
      - name: Display Node Setup Details
        shell: bash
        run: |
          echo "Working Directory: ${{ inputs.working-directory }}"
```

## Notes

- Before using this action, make sure to have `nvm` and `yarn` installed on the runner machine.
- The action uses `actions/setup-node@v3` to set up the specified Node.js version using the `.nvmrc` file.
- It then caches the Yarn cache directory using `actions/cache@v3` to speed up future installations.
- The action finally installs the project dependencies using Yarn with the `yarn install --immutable` command.

