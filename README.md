# Foundation Github Actions Workflows

![GitHub Actions Logo](https://github.githubassets.com/images/modules/site/features/actions-icon-actions.svg)

This repository provides Github Actions, [composite action](https://docs.github.com/en/actions/creating-actions/creating-a-composite-action) 
and reusable workflows.

## Table of contents

### Actions

- [Mend Scan Action](actions/mend-scan/README.md)
- [AWS Cognito Info](actions/aws-cognito-info/README.md)
- [AWS Docker Tag](actions/aws-docker-tag/README.md)
- [AWS S3 Deploy App](actions/aws-s3-deploy-app/README.md)
- [Configure AWS Credentials](actions/configure-aws-credentials/README.md)
- [Docker Deploy](actions/docker-deploy/README.md)
- [Node Setup](actions/node-setup/README.md)

### Workflows

- [AWS Docker Deploy](.github/workflows/aws-docker-deploy.md)

## Release process

To release a new version of the actions and workflows herein, simply follow the process to [create a release through GitHub](https://docs.github.com/en/repositories/releasing-projects-on-github/managing-releases-in-a-repository).
Taking the time to write a short summary of the changes to this version in the release description textbox would be nice for future users :wink:.

To keep the usage simple, we keep the version number to two digits: major (features) and minor (bug fixes, adjustments, etc). For example: "v1.1".

Once the release is created, update the version used within the repository where needed. See the [GitHub examples using versioned actions](https://docs.github.com/en/actions/using-workflows/workflow-syntax-for-github-actions#example-using-versioned-actions).
