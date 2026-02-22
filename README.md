# Docker Installation with Ansible

**Docker Ansible** is a simple, clean, and idempotent Ansible playbook to install and configure **Docker** + **Docker Compose plugin** (v2) on Ubuntu servers.

It adds the official Docker repository, installs the latest stable Docker packages, installs the Compose plugin, and adds the remote user to the docker group — so you can run `docker` commands without sudo.

![Docker](https://img.shields.io/badge/docker-ready-blue)
![Ubuntu](https://img.shields.io/badge/Ubuntu-supported-orange)
![Ansible](https://img.shields.io/badge/ansible-8.x+-blue)
![License](https://img.shields.io/badge/license-MIT-green)

<div align="center">
  <img src="https://www.docker.com/wp-content/uploads/2022/03/Moby-logo.png" alt="Docker Logo" width="180"/>
</div>

## What You Can Do

- Install Docker CE + containerd + Docker Compose v2 plugin automatically
- Add your SSH user to the docker group (no sudo needed for docker commands)
- Run on one or multiple Ubuntu servers using inventory
- Safe & idempotent — rerun anytime without issues
- Minimal dependencies and clean role structure

## Setup

### 1. Clone the repository

```bash
git clone https://github.com/YOUR_USERNAME/docker-ansible.git
cd docker-ansible
```

### 2. Install dependencies

Create & activate virtual environment (recommended):

```bash
python3 -m venv venv
source venv/bin/activate
```

Install Python packages:

```bash
pip install -r requirements.txt
```

Install required Ansible collection:

```bash
ansible-galaxy collection install community.docker
```

### 3. Configure inventory

Edit `inventory.ini` and put your server(s):

```ini
[docker]
srv1 ansible_host=192.168.1.100 ansible_user=ubuntu
```

### 4. Run the playbook

Basic run:

```bash
ansible-playbook -i inventory.ini playbook.yml
```

## What This Playbook Does

1. Installs prerequisites (`apt-transport-https`, `curl`, `gnupg`, etc.)
2. Adds official Docker GPG key
3. Adds Docker APT repository
4. Installs `docker-ce`, `docker-ce-cli`, `containerd.io`
5. Installs Docker Compose v2 plugin (`docker-compose-plugin`) if missing
6. Adds the remote SSH user to the `docker` group

After success, you can log in to the server and run:

```bash
docker --version
docker compose version
docker run hello-world
```

## Features

- Super simple — only one role
- Idempotent & safe to rerun
- Uses official Docker APT repository
- Installs modern Compose v2 (not old docker-compose binary)
- No hard-coded passwords or secrets

Enjoy containerizing! 🐳
