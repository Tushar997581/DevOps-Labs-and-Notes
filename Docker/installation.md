# 🛠️ Docker Installation

# Complete Docker Installation Guide for DevOps Engineers

Docker can be installed on Linux, Windows, and macOS. This guide follows the **official Docker installation methods** and covers installation, verification, configuration, upgrades, troubleshooting, and best practices.

> **Official Reference:** Docker Engine Installation Guide & Docker Desktop Documentation

---

# 🎯 Learning Objectives

After completing this guide, you will be able to:

- Understand Docker installation options
- Install Docker Engine on Linux
- Install Docker Desktop on Windows and macOS
- Install the Docker Compose plugin
- Verify Docker installation
- Manage the Docker service
- Run Docker without `sudo`
- Upgrade Docker
- Uninstall Docker
- Troubleshoot common installation problems

---

# 📖 Installation Options

Docker provides different installation methods depending on the operating system.

| Operating System | Recommended Installation |
|------------------|--------------------------|
| Ubuntu | Docker Engine |
| Debian | Docker Engine |
| RHEL | Docker Engine |
| CentOS Stream | Docker Engine |
| Fedora | Docker Engine |
| Amazon Linux 2023 | Docker Engine |
| Windows 10/11 | Docker Desktop |
| macOS | Docker Desktop |

---

# Docker Components Installed

Installing Docker typically installs:

```text
Docker Engine

│

├── Docker CLI

├── Docker Daemon (dockerd)

├── containerd

├── runc

└── Docker Compose Plugin
```

---

# Installation Workflow

```text
Download Docker

↓

Install Packages

↓

Start Docker Service

↓

Verify Installation

↓

Run First Container

↓

Ready for Development
```

---

# 🐧 Install Docker on Ubuntu

## Step 1 – Update Packages

```bash
sudo apt update
sudo apt upgrade -y
```

---

## Step 2 – Install Required Packages

```bash
sudo apt install -y \
ca-certificates \
curl \
gnupg
```

---

## Step 3 – Create Keyring Directory

```bash
sudo install -m 0755 -d /etc/apt/keyrings
```

---

## Step 4 – Add Docker's Official GPG Key

```bash
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | \
sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
```

Set permissions:

```bash
sudo chmod a+r /etc/apt/keyrings/docker.gpg
```

---

## Step 5 – Add Docker Repository

```bash
echo \
"deb [arch=$(dpkg --print-architecture) \
signed-by=/etc/apt/keyrings/docker.gpg] \
https://download.docker.com/linux/ubuntu \
$(. /etc/os-release && echo "$VERSION_CODENAME") stable" | \
sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```

---

## Step 6 – Update Repository

```bash
sudo apt update
```

---

## Step 7 – Install Docker

```bash
sudo apt install -y \
docker-ce \
docker-ce-cli \
containerd.io \
docker-buildx-plugin \
docker-compose-plugin
```

---

## Step 8 – Verify Installation

```bash
docker --version
```

Example

```text
Docker version 28.x.x
```

---

# 🟡 Install Docker on Debian

Follow the same official repository setup as Ubuntu, replacing the Ubuntu codename with the Debian release codename when adding the repository.

---

# 🔴 Install Docker on RHEL / Rocky Linux / AlmaLinux

Install the official Docker repository.

```bash
sudo dnf install -y dnf-plugins-core
```

Add the repository.

```bash
sudo dnf config-manager \
--add-repo https://download.docker.com/linux/rhel/docker-ce.repo
```

Install Docker.

```bash
sudo dnf install -y \
docker-ce \
docker-ce-cli \
containerd.io \
docker-buildx-plugin \
docker-compose-plugin
```

---

# 🔵 Install Docker on CentOS Stream

```bash
sudo dnf install docker-ce docker-ce-cli containerd.io \
docker-buildx-plugin docker-compose-plugin
```

---

# 🟠 Install Docker on Fedora

```bash
sudo dnf install docker-ce docker-ce-cli containerd.io \
docker-buildx-plugin docker-compose-plugin
```

---

# ☁️ Install Docker on Amazon Linux 2023

Update packages.

```bash
sudo dnf update -y
```

Install Docker.

```bash
sudo dnf install docker -y
```

Start Docker.

```bash
sudo systemctl enable --now docker
```

Verify.

```bash
docker --version
```

> **Note:** Package availability may vary depending on the Amazon Linux release. Always follow the official Amazon Linux and Docker documentation for your version.

---

# 🪟 Install Docker on Windows

Install **Docker Desktop**.

Requirements:

- Windows 10/11 (64-bit)
- WSL 2 enabled (recommended)
- Hardware virtualization enabled in BIOS/UEFI

Steps:

1. Download Docker Desktop.
2. Run the installer.
3. Enable WSL integration if prompted.
4. Restart the computer if required.
5. Open Docker Desktop.
6. Wait until Docker reports it is running.

Verify:

```powershell
docker --version
```

---

# 🍎 Install Docker on macOS

Install Docker Desktop.

Requirements:

- Apple Silicon (M-series) or Intel Mac
- Supported macOS version

Steps:

1. Download Docker Desktop.
2. Install the application.
3. Launch Docker Desktop.
4. Accept required permissions.
5. Wait for Docker to start.

Verify:

```bash
docker --version
```

---

# Start Docker Service

Linux

```bash
sudo systemctl start docker
```

Enable at boot.

```bash
sudo systemctl enable docker
```

Check status.

```bash
sudo systemctl status docker
```

---

# Run Docker Without sudo

Create the Docker group if needed.

```bash
sudo groupadd docker
```

Add your user.

```bash
sudo usermod -aG docker $USER
```

Apply the new group membership by logging out and back in, or start a new login session.

Verify.

```bash
docker ps
```

---

# Verify Installation

Check version.

```bash
docker --version
```

Check detailed information.

```bash
docker info
```

Verify Compose plugin.

```bash
docker compose version
```

---

# Run Your First Container

```bash
docker run hello-world
```

Expected output:

```text
Hello from Docker!
```

This confirms that Docker Engine is working correctly.

---

# Test with Nginx

```bash
docker run -d -p 8080:80 nginx
```

Verify.

```bash
docker ps
```

Open:

```text
http://localhost:8080
```

You should see the default Nginx welcome page.

---

# Docker Service Management

Start

```bash
sudo systemctl start docker
```

Stop

```bash
sudo systemctl stop docker
```

Restart

```bash
sudo systemctl restart docker
```

Status

```bash
sudo systemctl status docker
```

---

# Upgrade Docker

Ubuntu

```bash
sudo apt update
sudo apt upgrade
```

RHEL/Fedora

```bash
sudo dnf upgrade
```

Windows/macOS

Upgrade through Docker Desktop.

---

# Uninstall Docker

Ubuntu

```bash
sudo apt remove docker-ce docker-ce-cli containerd.io
```

Remove data (optional).

```bash
sudo rm -rf /var/lib/docker
sudo rm -rf /var/lib/containerd
```

> **Warning:** Removing these directories deletes containers, images, volumes, and local Docker data.

---

# Docker Installation Architecture

```text
                Docker Desktop

                      │

                Docker Engine

         ┌────────────┼────────────┐

         │            │            │

      Docker CLI   Docker Daemon  containerd

                      │

                     runc

                      │

                 Linux Kernel

                      │

                   Hardware
```

---

# Best Practices

✔ Install Docker from official repositories

✔ Keep Docker updated

✔ Enable automatic service startup on Linux

✔ Use the Docker Compose plugin instead of the legacy standalone `docker-compose` tool for new projects

✔ Verify installation after upgrades

✔ Use supported operating system versions

✔ Regularly update container images

---

# Common Installation Errors

## Docker Command Not Found

Verify installation.

```bash
docker --version
```

If Docker is not installed, complete the installation steps for your operating system.

---

## Cannot Connect to Docker Daemon

Start Docker.

```bash
sudo systemctl start docker
```

Verify.

```bash
sudo systemctl status docker
```

---

## Permission Denied

Add your user to the Docker group.

```bash
sudo usermod -aG docker $USER
```

Log out and log back in.

---

## Port Already in Use

Find the process using the port.

Linux

```bash
sudo ss -tulpn
```

Choose another port if necessary.

---

# Troubleshooting Checklist

- Docker installed successfully
- Docker service running
- User added to Docker group
- Docker CLI working
- Docker Compose plugin installed
- `hello-world` container runs successfully
- Internet connectivity available for pulling images

---

# Official Documentation

- Docker Engine Installation Guide
- Docker Desktop Documentation
- Docker CLI Reference
- Docker Compose Documentation
- Docker Engine Release Notes

---

# Quick Revision

```text
Docker Engine → Container Runtime

Docker CLI → User Interface

Docker Daemon → Background Service

containerd → Container Management

runc → OCI Runtime

docker --version → Check Version

docker info → System Information

docker run hello-world → Verify Installation

systemctl start docker → Start Service

docker compose version → Verify Compose Plugin
```

---

# Skills Covered

✔ Docker Installation

✔ Docker Desktop

✔ Docker Engine

✔ Docker Compose Plugin

✔ Docker Service Management

✔ First Container

✔ Verification

✔ Troubleshooting

---

# Screenshot Structure

```text
screenshots/

└── installation/

    ├── 01-download-docker.png
    ├── 02-install-packages.png
    ├── 03-start-docker-service.png
    ├── 04-docker-version.png
    ├── 05-docker-info.png
    ├── 06-hello-world.png
    ├── 07-nginx-container.png
    ├── 08-browser-output.png
    └── installation-complete-lab.png
```

---

# Related Topics

- Docker Architecture
- Docker Images
- Docker Containers
- Dockerfile
- Docker Compose
- Docker Networking
- Docker Volumes

---

# Status

🛠️ Docker Installation Completed ✅
