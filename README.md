# Github Workflows for Ansible Roles

## Continuous Integration (Molecule)

### Configuration

| Variable | Type | Default | Description |
|---|---|---|---|
| distros | string | '[ "debian11", "debian10" ]' | List of distributions to test against the Role |
| python-dependencies | string | [see workflow](.github/workflows/ansible-integration-workflow.yaml) | Default pip dependencies for molecule |
| role-dependencies | string | [see workflow](.github/workflows/ansible-integration-workflow.yaml) | Default role dependencies for ansible (empty)|
| molecule-config | string | [see workflow](.github/workflows/ansible-integration-workflow.yaml) | Configuration for molecule |
| disable-apparmor-mysql | boolean | false | Disable AppArmor MySQL Profile for the Job Runner |

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
    uses: systemli/github-ansible-workflow/.github/workflows/ansible-integration-workflow.yaml@main
    with:
      distros: '[ "debian11", "debian10", "ubuntu2204", "ubuntu2004", "ubuntu1804" ]'
    secrets:
      galaxy-token: ${{ secrets.galaxy_api_key }}
```

## Ansible Galaxy

### Configuration

| Variable | Type | Default | Description |
|---|---|---|---|
| galaxy-token | secret | | Secret for Ansible Galaxy |

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
