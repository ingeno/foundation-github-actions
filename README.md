# Foundation GitHub Actions Workflows

![GitHub Actions Logo](https://github.githubassets.com/images/modules/site/features/actions-icon-actions.svg)

This repository provides GitHub Actions, [composite actions](https://docs.github.com/en/actions/creating-actions/creating-a-composite-action) 
and reusable workflows.

## Table of contents

### Actions

- [AWS Cognito Info](actions/aws-cognito-info/README.md)
- [AWS Docker Tag](actions/aws-docker-tag/README.md)
- [AWS S3 Deploy App](actions/aws-s3-deploy-app/README.md)
- [Configure AWS Credentials](actions/configure-aws-credentials/README.md)
- [Docker Deploy](actions/docker-deploy/README.md)
- [Mend Scan Action](actions/mend-scan/README.md)
- [Node Setup](actions/node-setup/README.md)

### Workflows

- [AWS Docker Deploy](.github/workflows/aws-docker-deploy.md)

## Automatic Release Management

### Introduction

This section outlines the release management process established for the *Foundation GitHub Actions* project.
The release management approach ensures accurate and consistent versioning across all actions and workflows within
the repository.

### Release Philosophy

#### Workflow Initiation
To ensure accuracy throughout the release cycle and to avoid unnecessary version bumps,
releases are initiated manually.

#### Versioning
A unified versioning system is implemented for all actions, ensuring uniformity across the entire project.
This approach uses Lerna, which automatically adjusts the version of all actions and workflows in the monorepo.
As a result, all the previous are updated to the same version and are released simultaneously.

#### Release Condition
Only PRs labeled with `auto-release` activate the releasing workflow. This label is automatically added in the
`create-release-pr` workflow, which is triggered manually.

#### Actions Versioning & Changelog
With Lerna:
- Versions are automatically adjusted based on established commit conventions.
- A `CHANGELOG.md` is generated for every updated sub-package, detailing its changes.
- `lerna version` is the command responsible for versioning and changelog generation.
  For more details on the Lerna version command, visit [Lerna version command](https://github.com/lerna/lerna/tree/main/libs/commands/version#readme)

#### Pull Request for New Release
When a release is initiated, a Pull Request is created with the changelog and updated version. After this PR is
approved and merged, the associated workflow will generate a release note and create a release with the proper tag.
The unified versioning ensures a single release note and tag for the entire monorepo.

#### Commit Versioning
[Conventional commits](https://www.conventionalcommits.org/en/v1.0.0/) drive the version updates as follows:

- A `fix` commit results in a patch bump (e.g., 1.0.0 to 1.0.1).
- A `feat` commit results in a minor bump (e.g., 1.0.0 to 1.1.0).
- The presence of a `BREAKING CHANGE:` in the commit footer leads to a major bump (e.g., 1.0.0 to 2.0.0).
This is how your commit would look like with a breaking change in the footer:
```
<type>[optional scope]: <description>
<blank line>
<optional body>
<blank line>
<BREAKING CHANGE: Include description of your breaking change here>
```
### Release Steps

1. **Initiation**: Manually trigger the [Create Release PR](https://github.com/ingeno/foundation-github-actions/actions/workflows/create-release-pr.yml) workflow. This action bumps the version, generates the
   changelog, and initiates the creation of a Pull Request labeled `auto-release`.

   **Note**: Be aware that a pre-configured token named `FOUNDATION_START_RELEASE_TOKEN` with permissions to create pull requests is used in this workflow. While the default `GITHUB_TOKEN` can initiate the workflow, it may lead to checks that remain in a pending state due to its limitations in triggering other workflows. For more information, consult [GitHub Token Permissions](https://docs.github.com/en/actions/reference/authentication-in-a-workflow#permissions-for-the-github_token).

2. **Approval**: The PR must be approved. Post approval, an automated job is activated.
3. **Tag and Release Notes Generation**: After the PR is merged, a tag corresponding to the new version is established,
   and release notes are created.

### Commit Verification

Commit verification is a prerequisite in our process. As such, commits made during the CI/CD release process must be
signed using a GPG key. To facilitate this, we utilize the GitHub user `ci-ingeno` to sign the commits. A GPG key
was specifically generated for this account, with both the key and its passphrase stored in the [foundation vault](https://ingeno.1password.com/vaults/746pluvhck4djni6wlubkzaupi/allitems).
By employing a dedicated action, we can import this key and sign commits throughout the workflow.

For detailed guidance on this setup, please refer to this [blog post](https://httgp.com/signing-commits-in-github-actions/).
