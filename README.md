# Ansible Collection: rhoai.ai_workspace

Provision and manage self-service AI coding workspaces on OpenShift
using Red Hat OpenShift AI, ArgoCD, and Helm.

## Roles

| Role | Description |
|------|-------------|
| `rhoai.ai_workspace.provision` | Validate inputs, create an ArgoCD Application CR, wait for sync, and return the workspace route URL |
| `rhoai.ai_workspace.teardown` | Delete the ArgoCD Application CR and workspace namespace |

## Requirements

- Ansible >= 2.14
- `kubernetes.core` collection >= 2.4.0
- Authenticated `oc` / `kubectl` session with cluster-admin or scoped RBAC
- ArgoCD (OpenShift GitOps) with a tenant ArgoCD instance
- The `ai-workspace` Helm chart accessible from ArgoCD

## Installation

```bash
# From a local build
ansible-galaxy collection build .
ansible-galaxy collection install rhoai-ai_workspace-1.0.0.tar.gz

# Or reference directly in requirements.yml
```

## Usage

```yaml
- name: Provision AI Workspace
  hosts: localhost
  connection: local
  gather_facts: false
  roles:
    - role: rhoai.ai_workspace.provision
      vars:
        username: jbatchel
        git_repo: https://github.com/org/repo.git
        ai_model: qwen25-coder-14b
```

## Role Variables

See each role's `defaults/main.yml` for the full list of configurable
variables and their defaults.
