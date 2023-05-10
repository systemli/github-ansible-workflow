# Github Workflows for Ansible Roles

[![Integration](https://github.com/systemli/github-ansible-workflow/actions/workflows/integration.yml/badge.svg)](https://github.com/systemli/github-ansible-workflow/actions/workflows/integration.yml)

## Continuous Integration (Molecule)

### Configuration

| Variable               | Type    | Default                                                             | Description                                        |
| ---------------------- | ------- | ------------------------------------------------------------------- | -------------------------------------------------- |
| distros                | string  | '[ "debian11", "debian10" ]'                                        | List of distributions to test against the Role     |
| python-dependencies    | string  | [see workflow](.github/workflows/ansible-integration-workflow.yaml) | Default pip dependencies for molecule              |
| molecule-config        | string  | [see workflow](.github/workflows/ansible-integration-workflow.yaml) | Configuration for molecule                         |
| disable-apparmor-mysql | boolean |  false                                                              |  Disable AppArmor MySQL Profile for the Job Runner |

### Usage

Create a workflow, e.g. `.github/workflows/integration.yaml`

```yaml
---
name: Integration

on:
  push:
    branches:
      - main
  pull_request:

jobs:
  integration:
    name: Integration
    uses: systemli/github-ansible-workflow/.github/workflows/ansible-integration-workflow.yaml@v1.0.0
    with:
      distros: '[ "debian11", "debian10", "ubuntu2204", "ubuntu2004", "ubuntu1804" ]'
```

## Ansible Galaxy

### Configuration

| Variable     | Type   | Default | Description               |
| ------------ | ------ | ------- | ------------------------- |
| galaxy-token | secret |         | Secret for Ansible Galaxy |

### Usage

Create a workflow, e.g. `.github/workflows/galaxy.yaml`

```yaml
---
name: Ansible Galaxy

on:
  push:
    branches:
      - main
  release:

jobs:
  galaxy:
    name: Ansible Galaxy
    uses: systemli/github-ansible-workflow/.github/workflows/ansible-galaxy-workflow.yaml@main
    secrets:
      galaxy-token: ${{ secrets.galaxy_api_key }}
```
