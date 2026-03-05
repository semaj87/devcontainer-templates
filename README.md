# Devcontainer-templates

Personal DevPod devcontainer templates for Python, AWS, Kubernetes, and Neovim practice environments. Used with [DevPod](https://devpod.sh) to spin up reproducible, isolated development containers.

---

## Templates

### python-aws
For professional Python development with AWS tooling. Used for work repos cloned from GitLab.

**Includes:**
- Python 3.12 (change image tag to match repo requirements e.g. `3.9`, `3.10`, `3.11`)
- Poetry
- AWS CLI
- awsume
- Terraform
- Node.js
- Claude Code
- Neovim
- Zsh + oh-my-zsh + Powerlevel10k

**AWS credentials** are mounted read-only from `~/.aws` on the host Mac.

**Usage:**
```bash
git clone git@gitlab.com:your-org/some-repo.git ~/work/some-repo
cp -R ~/devcontainer-templates/python-aws/.devcontainer ~/work/some-repo/
cd ~/work/some-repo
devpod up .
devpod ssh some-repo
```

**To change Python version**, update the image tag in the Dockerfile:
```dockerfile
FROM mcr.microsoft.com/devcontainers/python:3.11
```

---

### python
Lightweight Python environment for personal projects and learning.

**Includes:**
- Python 3.12
- Poetry
- Neovim
- Zsh + oh-my-zsh + Powerlevel10k

**Usage:**
```bash
mkdir ~/personal/my-project
cd ~/personal/my-project
cp -R ~/devcontainer-templates/python/.devcontainer .
devpod up .
devpod ssh my-project
```

---

### kubernetes
Kubernetes tooling environment for interacting with and learning about k8s clusters.

**Includes:**
- kubectl
- Helm
- k9s
- kubectx / kubens
- stern
- AWS CLI (for EKS authentication)
- awsume
- Neovim
- Zsh + oh-my-zsh + Powerlevel10k

**Kubeconfig** is mounted from `~/.kube` on the host Mac.
**AWS credentials** are mounted read-only from `~/.aws` on the host Mac.

**Usage:**
```bash
mkdir ~/personal/k8s-practice
cd ~/personal/k8s-practice
cp -R ~/devcontainer-templates/kubernetes/.devcontainer .
devpod up .
devpod ssh k8s-practice
```

---

### nvim-practice
Throwaway environment for learning and practising Neovim without risk to the host machine. Delete and recreate freely.

**Includes:**
- Neovim (latest)
- Zsh + oh-my-zsh + Powerlevel10k
- Full Neovim config from dotfiles

**Usage:**
```bash
mkdir ~/personal/nvim-practice
cd ~/personal/nvim-practice
cp -R ~/devcontainer-templates/nvim-practice/.devcontainer .
devpod up .
devpod ssh nvim-practice
```

When done:
```bash
devpod delete nvim-practice
```

---

## How Dotfiles Work

Every template clones the [dotfiles repo](https://github.com/semaj87/dotfiles) and runs `install.sh` automatically via `postCreateCommand`. This means every container gets:

- Zsh config with Powerlevel10k prompt
- Neovim config with full plugin setup
- Git config
- Shell aliases

No manual setup needed after `devpod up .`.

---

## DevPod Workflow

```bash
# Start a container
devpod up .

# SSH into a running container
devpod ssh workspace-name

# Stop a container (preserves state)
devpod stop workspace-name

# Start a stopped container
devpod up workspace-name

# Delete a container (frees disk space)
devpod delete workspace-name

# List all containers
devpod list

# Force rebuild from scratch
devpod up . --recreate
```

## IDE Options

Each container supports two ways of working:

### SSH (terminal only)
Best for lightweight containers like nvim-practice and kubernetes where you just need a terminal:
```bash
devpod ssh workspace-name
```

### PyCharm via JetBrains Gateway
Best for work repos in python-aws where you need a full IDE experience with debugging, refactoring, and test running. Requires [JetBrains Gateway](https://www.jetbrains.com/remote-development/gateway/) installed via JetBrains Toolbox.
```bash
devpod up . --ide pycharm
```

Gateway connects PyCharm running on your Mac to the container backend. The first connection downloads the PyCharm backend into the container (~700MB) which only happens once — subsequent connections are instant.

To default to SSH and only use PyCharm when needed, set the default IDE to **None** in DevPod settings and pass `--ide pycharm` explicitly when required.

---

## Repository Structure

```
devcontainer-templates/
├── python-aws/
│   └── .devcontainer/
│       ├── devcontainer.json
│       └── Dockerfile
├── python/
│   └── .devcontainer/
│       └── devcontainer.json
├── kubernetes/
│   └── .devcontainer/
│       ├── devcontainer.json
│       └── Dockerfile
└── nvim-practice/
    └── .devcontainer/
        ├── devcontainer.json
        └── Dockerfile
```
