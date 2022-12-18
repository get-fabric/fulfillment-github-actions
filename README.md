# fulfillment-github-actions

This repository holds GitHub workflows that are commonly used by fulfillment V2 services.

See below for more information on specific workflows.


## update-integration-environment
This repository is a GitHub workflow that is used to load services k8s definitions into the [integration-environment](https://github.com/get-fabric/integration-environment) repo.

### Usage

To add a service to the integration environment add a workflow named `update-integration-environment.yml` to your service github workflows folder:
```
name: update-integration-environment

on:
  push:
    paths:
      - 'deployment/**'
    branches: [main]

  workflow_dispatch:

jobs:
  execute:
    uses: get-fabric/fulfillment-github-actions/.github/workflows/update-integration-environment.yaml@main
    if: ${{ github.event.head_commit.message != 'initial commit' }}
    with:
      namespace: fulfillment
    secrets:
      github_api_token: ${{ secrets.ORG_GITHUB_ADMIN_TOKEN }}
```
