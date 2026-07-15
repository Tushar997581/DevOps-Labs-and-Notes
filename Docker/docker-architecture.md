# 🏗️ Docker Architecture

# Complete Docker Architecture Guide for DevOps Engineers

Docker follows a **client-server architecture** where the Docker Client communicates with the Docker Engine (Docker Daemon) using the Docker REST API. The daemon is responsible for building images, creating containers, managing storage, configuring networking, and interacting with container runtimes.

Docker is built on Linux kernel features such as **Namespaces**, **cgroups**, **OverlayFS**, and follows the **Open Container Initiative (OCI)** specifications for container images and runtimes.

> **Official References**
>
> - Docker Engine Documentation
> - Docker CLI Documentation
> - Docker Build Documentation
> - OCI Runtime Specification
> - OCI Image Specification

---

# 🎯 Learning Objectives

After completing this guide, you will understand:

- Docker Architecture
- Docker Engine
- Docker Client
- Docker Daemon
- Docker REST API
- containerd
- runc
- Docker Images
- Docker Containers
- BuildKit
- OverlayFS
- Linux Namespaces
- Linux cgroups
- OCI Standards
- Production Architecture

---

# Why Learn Docker Architecture?

Most developers know this command:

```bash
docker run nginx
```

Very few understand what happens internally.

Understanding Docker Architecture helps you:

- Debug production issues
- Optimize performance
- Secure containers
- Troubleshoot Kubernetes
- Understand container runtimes

---

# High-Level Architecture

```text
                  Developer

                      │

                docker CLI

                      │

               REST API Request

                      │

              Docker Daemon

        ┌─────────────┼─────────────┐

        │             │             │

     Images      Containers     Networks

        │             │             │

        └─────────────┼─────────────┘

                      │

                 containerd

                      │

                     runc

                      │

                Linux Kernel

                      │

                  Hardware
```

---

# Docker Components

```text
Docker

│

├── Docker Client

├── Docker Engine

├── Docker Daemon

├── Docker REST API

├── containerd

├── runc

├── Images

├── Containers

├── Networks

├── Volumes

└── Registry
```

---

# Docker Client (CLI)

The Docker Client is the command-line interface used by users.

Example:

```bash
docker run nginx
```

When this command is executed:

1. CLI validates the syntax.
2. CLI sends a REST API request.
3. Docker Daemon receives the request.
4. Daemon performs the requested operation.

The CLI itself does **not** create containers.

---

# Docker REST API

Docker CLI communicates with Docker Daemon using the Docker REST API.

```text
docker run nginx

↓

REST API

↓

Docker Daemon
```

Other tools (such as IDEs or automation platforms) can also interact with Docker through this API.

---

# Docker Daemon (dockerd)

The Docker Daemon is the main background service.

Responsibilities:

- Build Images
- Pull Images
- Push Images
- Create Containers
- Start Containers
- Stop Containers
- Manage Networks
- Manage Volumes
- Manage BuildKit
- Communicate with Registries

Check status:

```bash
sudo systemctl status docker
```

---

# Docker Engine

Docker Engine includes:

```text
Docker Engine

│

├── Docker CLI

├── Docker Daemon

└── REST API
```

It is responsible for the complete container lifecycle.

---

# containerd

`containerd` is an industry-standard container runtime responsible for managing the lifecycle of containers.

Responsibilities:

- Image Management
- Snapshot Management
- Container Lifecycle
- Task Execution

Docker uses `containerd` internally.

Kubernetes can also use `containerd` directly.

---

# runc

`runc` is the low-level OCI runtime.

Responsibilities:

- Create Containers
- Start Processes
- Configure Linux Namespaces
- Configure cgroups

Docker → containerd → runc

---

# Request Flow

When running:

```bash
docker run nginx
```

The sequence is:

```text
docker CLI

↓

REST API

↓

Docker Daemon

↓

containerd

↓

runc

↓

Linux Kernel

↓

Container Started
```

---

# Docker Image Architecture

A Docker Image is built from layers.

Example

```text
Application

↓

Python

↓

Ubuntu

↓

Scratch
```

Each Dockerfile instruction typically creates a new immutable layer.

Benefits:

✔ Layer Reuse

✔ Faster Builds

✔ Smaller Downloads

✔ Efficient Caching

---

# OverlayFS

Docker commonly uses **OverlayFS** (or another supported storage driver depending on the platform) to combine image layers into a single unified filesystem.

```text
Layer 4

Application

------------

Layer 3

Python

------------

Layer 2

Ubuntu Packages

------------

Layer 1

Base Image
```

When a container starts:

```text
Image Layers

↓

Writable Layer

↓

Running Container
```

Only the writable layer changes during container execution.

---

# Docker Container Lifecycle

```text
docker create

↓

Created

↓

docker start

↓

Running

↓

docker stop

↓

Stopped

↓

docker rm

↓

Deleted
```

---

# Linux Namespaces

Namespaces provide isolation.

Types:

- PID Namespace
- Network Namespace
- Mount Namespace
- User Namespace
- IPC Namespace
- UTS Namespace

Each container receives isolated resources.

Example:

```text
Container A

PID 1

Container B

PID 1
```

Both containers have their own process tree.

---

# Linux cgroups

Control Groups (cgroups) limit resources.

Examples:

```text
CPU

Memory

Disk

Network
```

Without cgroups:

```text
Container

↓

Uses 100% CPU
```

With cgroups:

```text
Container

↓

2 CPUs

↓

2 GB RAM
```

---

# BuildKit

BuildKit is Docker's modern image builder.

Benefits:

- Faster Builds
- Parallel Execution
- Better Caching
- Secret Management
- Multi-stage Optimization

BuildKit is enabled by default in modern Docker releases.

---

# Docker Networking

Every container communicates through Docker networking.

Network Types:

```text
Bridge

Host

None

Overlay

Macvlan
```

Default:

Bridge Network

---

# Docker Storage

Docker supports:

- Volumes
- Bind Mounts
- tmpfs Mounts

Storage should be externalized for persistent application data.

---

# Docker Registry

Image workflow:

```text
Dockerfile

↓

docker build

↓

Image

↓

docker push

↓

Registry

↓

docker pull

↓

Container
```

Popular registries:

- Docker Hub
- Amazon ECR
- GitHub Container Registry
- Azure Container Registry

---

# OCI Standards

Docker follows the Open Container Initiative (OCI) standards.

OCI defines:

- Image Format
- Runtime Specification
- Distribution Specification

This enables compatibility across different runtimes and registries.

---

# What Happens During `docker run`?

```text
docker run nginx

↓

Check Local Image

↓

Pull Image (if missing)

↓

Create Writable Layer

↓

Configure Network

↓

Mount Filesystem

↓

Configure cgroups

↓

Configure Namespaces

↓

Start Process

↓

Container Running
```

---

# Production Architecture

```text
Developer

↓

Git Repository

↓

CI/CD Pipeline

↓

Docker Build

↓

Security Scan

↓

Docker Registry

↓

Kubernetes Cluster

↓

containerd

↓

runc

↓

Linux Kernel

↓

Production Containers
```

---

# Security Architecture

Docker provides isolation through:

- Namespaces
- cgroups
- Linux Capabilities
- seccomp
- AppArmor / SELinux (platform dependent)
- Rootless Mode (supported environments)

Best practices:

✔ Use official images

✔ Avoid privileged containers

✔ Drop unnecessary Linux capabilities

✔ Enable image scanning

✔ Use non-root users

✔ Keep images updated

---

# Common Mistakes

❌ Running containers as root

❌ Using `latest` in production

❌ Large Docker Images

❌ Hardcoding secrets

❌ Ignoring health checks

❌ Ignoring resource limits

---

# Troubleshooting

## Docker Daemon Down

```bash
sudo systemctl status docker
```

---

## Cannot Connect

```bash
docker info
```

Verify that the Docker daemon is running and that your user has permission to access it.

---

## High Disk Usage

```bash
docker system df
```

Clean unused resources carefully:

```bash
docker system prune
```

---

## Container Keeps Restarting

Investigate:

```bash
docker logs <container-name>
docker inspect <container-name>
```

Check:

- Application errors
- Environment variables
- Health checks
- Port conflicts
- Resource limits

---

# Interview Questions

### What is Docker Architecture?

Docker follows a client-server architecture where the Docker Client communicates with the Docker Daemon through the Docker REST API.

---

### What is containerd?

containerd is the container runtime responsible for image management, snapshot management, and container lifecycle operations.

---

### What is runc?

runc is the low-level OCI runtime that creates and starts containers using Linux kernel features.

---

### What are Linux Namespaces?

Namespaces isolate processes and other system resources so that containers operate independently.

---

### What are cgroups?

cgroups control and limit resource usage such as CPU and memory for containers.

---

### What is OverlayFS?

OverlayFS is a layered filesystem used by Docker (on supported Linux systems) to efficiently combine image layers and a writable container layer.

---

### What is BuildKit?

BuildKit is Docker's build engine that improves performance, caching, and advanced build capabilities.

---

### What is OCI?

The Open Container Initiative defines open standards for container images and runtimes.

---

# Official Documentation

- Docker Engine Documentation
- Docker CLI Documentation
- Docker Build Documentation
- Docker Storage Documentation
- Docker Networking Documentation
- OCI Image Specification
- OCI Runtime Specification

---

# Quick Revision

```text
Docker CLI → User Interface

REST API → Communication

Docker Daemon → Background Service

Docker Engine → Core Runtime

containerd → Container Lifecycle

runc → OCI Runtime

Namespaces → Isolation

cgroups → Resource Limits

OverlayFS → Layered Filesystem

OCI → Container Standards
```

---

# Skills Covered

✔ Docker Architecture

✔ Docker Engine

✔ Docker Daemon

✔ Docker Client

✔ REST API

✔ containerd

✔ runc

✔ OverlayFS

✔ Namespaces

✔ cgroups

✔ OCI Standards

✔ Production Docker Workflow

---

# Screenshot Structure

```text
screenshots/

docker-architecture/

├── 01-docker-engine.png
├── 02-client-daemon.png
├── 03-containerd-runtime.png
├── 04-image-layers.png
├── 05-overlayfs.png
├── 06-docker-network.png
├── 07-container-lifecycle.png
├── 08-production-architecture.png
└── docker-architecture-complete-lab.png
```

---

# Related Topics

- Docker Installation
- Docker Images
- Docker Containers
- Dockerfile
- Docker Networks
- Docker Volumes
- Docker Compose
- Kubernetes Container Runtime

---

# Status

🏗️ Docker Architecture Completed ✅
