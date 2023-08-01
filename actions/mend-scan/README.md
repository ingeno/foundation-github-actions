# mend-scan

To ensure compliance with licenses for open-source third-party libraries used in a project, this GitHub Action can be run as part of your workflow. It uses the [Mend Unified Agent](https://docs.mend.io/bundle/unified_agent/page/overview_of_the_unified_agent.html) to scan for license compliance, which allows for better control of which third-party libraries are included either directly or transitively.

## Using the GitHub Action

The Mend Scan Action can be run as a step in your workflows, for example the `Pull Request Merged` workflow. It requires a few inputs to be set which you can find the list of those defined inputs and their descriptions [here](./action.yml) in the `inputs` section. Below is an example of including this action inside of an existing workflow:

```yml
name: Some Workflow

...

jobs:
  scan:
    name: scan
    runs-on: ubuntu-latest
    steps:
      - name: Checkout
        uses: actions/checkout@v3

      - name: Setup Node
        uses: ingeno/aws-workflows/.github/actions/node-setup@v1

      - name: Mend Scanner
        uses: ingeno/mend-scan-action@v1
        with:
          api-key: ${{secrets.WS_APIKEY}}
          product-token: ${{secrets.WS_PRODUCTTOKEN}}
          update-inventory: true
          yarn-workspaces: true
          log-level: trace

...

```

### Prerequisites

Before you can run the action you must have at least a product created on the Mend Web App or through the SCA API. Once you have a product created, you will be able to copy the Product Token from the Product Settings page or the Integrate page and add it as a variable in your Github repo or pass it directly as an input (`product-token`) as shown above.

### Additional Configuration

As defined in the `inputs` section in the [action.yml](./action.yml) file, there is an input (`config-file`) for a configuration file that can take in additional parameters to customize the scanner runs. You can define as many of these files as needed (e.g. a file per environment) and depending on which file you need for a specific run, you can pass that as an input when invoking the action. An example of this configuration can be found below:

```
fileSystemScan=false
forceCheckAllDependencies=true
projectPerFolder=true
projectPerFolderIncludes=common/mocks,common/types,backend/api,frontend/admin,frontend/client,infra/aws,tools/eslint-config,tools/jest-utils-react
resolveAllDependencies=false
npm.resolveDependencies=true
npm.runPreStep=true
npm.yarnProject=true
npm.resolveLockFile=true
npm.projectNameFromDependencyFile=true
```

For more details on the parameters available and their functions, please visit the Mend documentation for [Unified Agent Configuration Parameters](https://docs.mend.io/bundle/unified_agent/page/unified_agent_configuration_parameters.html).

Note: In order to use the parameter `npm.projectNameFromDependencyFile=true` along with the `projectPerFolder=true`, you need to explicitly declare the version of each of the sub-projects in their corresponding `package.json` file.