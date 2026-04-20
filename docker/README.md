# 🐳 Install Docker — Ansible Playbook

> Automates the installation and configuration of **Docker Engine** on remote Linux hosts using Ansible.

---

## 📋 Table of Contents

- [Overview](#overview)
- [Prerequisites](#prerequisites)
- [Directory Structure](#directory-structure)
- [Playbook Details](#playbook-details)
- [Variables](#variables)
- [Usage](#usage)
- [Verification](#verification)
- [Troubleshooting](#troubleshooting)

---

## Overview

This playbook (`install_docker.yml`) automates the end-to-end installation of **Docker Engine** on one or more Linux hosts. It handles:

- Removing any conflicting/old Docker packages
- Adding the official Docker APT/YUM repository
- Installing Docker Engine, CLI, and containerd
- Enabling and starting the Docker service
- (Optional) Adding a non-root user to the `docker` group

---

## Prerequisites

| Requirement | Details |
|---|---|
| **Ansible** | >= 2.10 |
| **Python** | >= 3.6 on the control node |
| **Target OS** | Ubuntu 20.04+, Debian 11+, RHEL/CentOS 8+ |
| **SSH Access** | Passwordless SSH or valid credentials configured |
| **Privilege** | `become: true` — sudo access required on target hosts |

---

## Directory Structure

```
ansible/
└── playbooks/
    └── docker/
        ├── install_docker.yml   # Main playbook
        └── README.md            # This file
```

---

## Playbook Details

The playbook performs the following tasks in order:

1. **Uninstall old versions** — Removes `docker`, `docker.io`, `docker-engine`, and conflicting packages.
2. **Install dependencies** — Installs `ca-certificates`, `curl`, `gnupg`, and `lsb-release`.
3. **Add Docker GPG key** — Downloads and stores the official Docker GPG key.
4. **Add Docker repository** — Configures the stable Docker APT/YUM repository.
5. **Install Docker Engine** — Installs `docker-ce`, `docker-ce-cli`, and `containerd.io`.
6. **Enable & start service** — Ensures `docker` service is enabled on boot and currently running.
7. **Add user to docker group** *(optional)* — Allows a specified user to run Docker without `sudo`.

---

## Variables

You can customize the playbook behaviour using the following variables:

| Variable | Default | Description |
|---|---|---|
| `docker_user` | `""` | Username to add to the `docker` group (optional) |
| `docker_edition` | `ce` | Docker edition: `ce` (Community) or `ee` (Enterprise) |
| `docker_package_state` | `present` | Ansible package state: `present`, `latest` |
| `docker_service_state` | `started` | Service state after install |
| `docker_service_enabled` | `true` | Whether to enable Docker on boot |

You can override variables using the `--extra-vars` flag or by defining them in your inventory/group vars.

---

## Usage

### 1. Configure your inventory

Create or update your Ansible inventory file (e.g., `inventory.ini`):

```ini
[docker_hosts]
192.168.1.10 ansible_user=ubuntu ansible_ssh_private_key_file=~/.ssh/id_rsa
192.168.1.11 ansible_user=ubuntu ansible_ssh_private_key_file=~/.ssh/id_rsa
```

### 2. Run the playbook

```bash
ansible-playbook -i inventory.ini playbooks/docker/install_docker.yml
```

### 3. Run with privilege escalation (sudo)

```bash
ansible-playbook -i inventory.ini playbooks/docker/install_docker.yml --become
```

### 4. Limit to specific hosts

```bash
ansible-playbook -i inventory.ini playbooks/docker/install_docker.yml --limit 192.168.1.10
```

### 5. Override variables at runtime

```bash
ansible-playbook -i inventory.ini playbooks/docker/install_docker.yml \
  --extra-vars "docker_user=ubuntu docker_package_state=latest"
```

### 6. Dry run (check mode)

```bash
ansible-playbook -i inventory.ini playbooks/docker/install_docker.yml --check
```

---

## Verification

After the playbook runs, SSH into a target host and verify:

```bash
# Check Docker version
docker --version

# Verify service is running
sudo systemctl status docker

# Run a test container
docker run hello-world
```

Expected output for `docker --version`:
```
Docker version 25.x.x, build xxxxxxx
```

---

## Troubleshooting

| Issue | Solution |
|---|---|
| `Permission denied` connecting to Docker socket | Ensure the user was added to the `docker` group and re-login |
| `Repository not found` error | Verify internet access on the target host and that GPG key was added correctly |
| `Package not found` error | Run `apt-get update` manually on the target or set `update_cache: true` in the task |
| Playbook fails on `become` | Ensure the SSH user has passwordless sudo or pass `--ask-become-pass` |

---

## Related Resources

- [Docker Official Documentation](https://docs.docker.com/engine/install/)
- [Ansible Documentation](https://docs.ansible.com/)
- [Ansible `community.docker` Collection](https://docs.ansible.com/ansible/latest/collections/community/docker/)

---

> **Author:** Ajay  
> **Last Updated:** April 2026
