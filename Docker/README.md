# 🐳 Docker

# Complete Docker Guide for DevOps Engineers

Docker is an open-source containerization platform that enables developers to build, package, ship, and run applications inside lightweight, portable environments called **containers**.

Docker solves one of the biggest software deployment challenges:

> **"It works on my machine."**

By packaging an application together with its runtime, libraries, dependencies, and configuration files, Docker ensures that applications behave consistently across development, testing, and production environments.

Today Docker is one of the core technologies behind:

- Microservices
- Kubernetes
- CI/CD Pipelines
- Cloud Computing
- DevOps
- Platform Engineering

Docker follows the **Open Container Initiative (OCI)** standards, making container images and runtimes interoperable across different platforms.

---

# 📖 What is Docker?

Docker is a **containerization platform**.

It allows applications to run inside isolated environments called **containers**.

Unlike Virtual Machines, Docker containers **share the host operating system kernel**, making them lightweight and extremely fast.

Example

```text
Application

↓

Docker Image

↓

Docker Container

↓

Runs Anywhere
```

---

# Learning Objectives

After completing this guide you will understand

- Docker
- Containerization
- Docker Architecture
- Docker Engine
- Docker Daemon
- Docker Client
- Docker Images
- Docker Containers
- Docker Registry
- Docker Networking
- Docker Storage
- OCI Standards
- Production Docker Workflow
- Docker Best Practices

---

# Why Docker?

Imagine a Python application.

Developer Laptop

```text
Python 3.12

Flask

Redis

Works Perfectly
```

Production Server

```text
Python 3.9

Old Libraries

Application Crash
```

This happens because environments are different.

Docker packages everything together.

```text
Application

↓

Dependencies

↓

Runtime

↓

Docker Image

↓

Container

↓

Runs Identically Everywhere
```

Benefits

✔ Consistent Environment

✔ Fast Deployment

✔ Portability

✔ Scalability

✔ Isolation

✔ Easy Rollback

✔ Better Resource Utilization

---

# What is Containerization?

Containerization is the process of packaging:

- Application
- Runtime
- Libraries
- Dependencies
- Configuration

into a single executable unit called a **Container**.

Example

```text
Python App

↓

Docker Image

↓

Docker Container

↓

Laptop

↓

AWS EC2

↓

Azure VM

↓

Google Cloud

↓

Kubernetes
```

Same application.

Same behavior.

Different environments.

---

# Virtual Machines vs Containers

Traditional Virtualization

```text
Application

↓

Guest OS

↓

Hypervisor

↓

Host OS

↓

Hardware
```

Containerization

```text
Application

↓

Container Runtime

↓

Host Operating System

↓

Hardware
```

Containers remove the need for a complete Guest Operating System.

---

# Docker vs Virtual Machine

| Feature | Virtual Machine | Docker Container |
|----------|-----------------|------------------|
| Guest OS | Required | Not Required |
| Startup Time | Minutes | Seconds |
| Image Size | GB | MB |
| Memory Usage | High | Low |
| Performance | Lower | Near Native |
| Isolation | Strong | Process Isolation |
| Portability | Moderate | Excellent |

---

# Docker Architecture

Docker uses a **client-server architecture**.

```text
                    Developer

                        │

                  Docker CLI

                        │

             REST API Request

                        │

                Docker Daemon

        ┌───────────────┼───────────────┐

        │               │               │

     Images        Containers      Networks

        │               │               │

        └───────────────┼───────────────┘

                        │

                 Linux Kernel

                        │

                  Host Hardware
```

---

# Docker Components

Docker consists of several components.

```text
Docker

│

├── Docker Client

├── Docker Daemon

├── Docker Engine

├── Docker Images

├── Docker Containers

├── Docker Registry

├── Docker Networks

├── Docker Volumes

└── BuildKit
```

---

# Docker Client

The Docker Client is the command-line interface (CLI) used by users.

Example

```bash
docker run nginx
```

The CLI sends REST API requests to the Docker Daemon.

---

# Docker Daemon

The Docker Daemon (`dockerd`) is the background service that manages Docker objects.

Responsibilities

- Build Images
- Run Containers
- Manage Networks
- Manage Volumes
- Pull Images
- Push Images
- Handle Registries

The daemon continuously listens for API requests.

---

# Docker Engine

Docker Engine is the core runtime.

It includes

- Docker CLI
- Docker Daemon
- REST API

Docker Engine is responsible for managing the complete container lifecycle.

---

# Docker REST API

Docker CLI communicates with Docker Daemon using the Docker REST API.

Example

```text
docker run nginx

↓

Docker CLI

↓

REST API

↓

Docker Daemon

↓

Container Created
```

This architecture also allows external tools to interact with Docker programmatically.

---

# Docker Images

A Docker Image is a read-only template.

It contains

- Application
- Runtime
- Libraries
- Packages
- Configuration

Images are built using a **Dockerfile**.

Example

```text
Dockerfile

↓

docker build

↓

Docker Image

↓

docker run

↓

Container
```

---

# Docker Containers

A container is a running instance of an image.

Example

```text
Ubuntu Image

↓

docker run ubuntu

↓

Ubuntu Container
```

Containers are:

- Lightweight
- Portable
- Isolated
- Temporary by default

---

# Docker Registry

A Docker Registry stores Docker Images.

Examples

- Docker Hub
- Amazon Elastic Container Registry (ECR)
- GitHub Container Registry (GHCR)
- Azure Container Registry (ACR)

Workflow

```text
Build Image

↓

Push

↓

Registry

↓

Pull

↓

Run Container
```

---

# Docker Image Layers

Docker Images are built using layers.

Example

```text
Ubuntu

↓

Python

↓

Flask

↓

Application
```

Every instruction in a Dockerfile creates a new layer (where applicable), enabling layer caching and efficient image distribution.

Benefits

✔ Smaller Downloads

✔ Faster Builds

✔ Layer Reuse

---

# Docker Lifecycle

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

docker run

↓

Container

↓

docker stop

↓

docker rm
```

---

# How Docker Works Internally

When you execute:

```bash
docker run nginx
```

Docker performs the following steps:

1. Checks if the image exists locally.
2. Pulls the image from the registry if necessary.
3. Creates a writable container layer.
4. Configures networking.
5. Configures storage.
6. Starts the container process.
7. Streams logs to Docker.

---

# Linux Technologies Behind Docker

Docker relies on Linux kernel features.

## Namespaces

Namespaces isolate resources.

Examples

- Process IDs (PID)
- Network
- Mount Points
- Users
- Hostname

Each container gets its own isolated view.

---

## Control Groups (cgroups)

Control Groups limit resource usage.

Examples

- CPU
- Memory
- Disk I/O
- Network

This prevents one container from consuming all host resources.

---

## Union File System

Docker uses layered file systems.

Example

```text
Ubuntu Layer

↓

Python Layer

↓

Application Layer

↓

Writable Layer
```

Only the top writable layer changes when the container runs.

---

# OCI Standards

Docker follows the Open Container Initiative standards.

OCI defines:

- Image Specification
- Runtime Specification
- Distribution Specification

This enables compatibility with runtimes such as **containerd** and **CRI-O**.

---

# Production Docker Workflow

```text
Developer

↓

GitHub

↓

CI/CD Pipeline

↓

docker build

↓

Docker Image

↓

Security Scan

↓

Docker Registry

↓

Kubernetes

↓

Production
```

---

# Docker in DevOps

Docker is used for

✔ Microservices

✔ CI/CD

✔ Kubernetes

✔ Testing

✔ Cloud Deployments

✔ Local Development

✔ Platform Engineering

---

# Best Practices

✔ Use official base images

✔ Keep images small

✔ Use multi-stage builds

✔ Avoid running containers as root

✔ Use `.dockerignore`

✔ Pin image versions instead of `latest`

✔ Scan images regularly

✔ Store secrets outside images

✔ Keep containers immutable

✔ Monitor logs and resource usage

---

# Common Docker Commands

```bash
docker version

docker info

docker pull nginx

docker images

docker run nginx

docker ps

docker stop

docker start

docker restart

docker logs

docker exec -it

docker inspect

docker rm

docker rmi
```

---

# Common Mistakes

❌ Using `latest` in production

❌ Running containers as root

❌ Storing secrets inside images

❌ Creating very large images

❌ Ignoring health checks

❌ Not cleaning unused images

---

# Troubleshooting

## Docker Daemon Not Running

```bash
sudo systemctl status docker
```

Start Docker

```bash
sudo systemctl start docker
```

---

## Permission Denied

```bash
sudo usermod -aG docker $USER
```

Log out and back in for the group change to take effect.

---

## Port Already Allocated

Find the process using the port or choose another port mapping.

---

## No Space Left on Device

Clean unused resources:

```bash
docker system prune
```

Review what will be removed before confirming.

---

# Real Production Architecture

```text
                  Developer

                       │

                  GitHub Repo

                       │

                GitHub Actions

                       │

                Docker Build

                       │

               Security Scan

                       │

             Docker Registry

                       │

               Kubernetes

          ┌────────────┼────────────┐

          │            │            │

     Container     Container    Container

          │            │            │

             Production Users
```

---

# Interview Questions

### What is Docker?

Docker is an open-source containerization platform used to package and run applications in isolated containers.

---

### What is the difference between an Image and a Container?

An Image is a read-only template.

A Container is a running instance of an Image.

---

### What is Docker Engine?

Docker Engine is the runtime that includes the Docker Daemon, Docker CLI, and REST API.

---

### What are Namespaces?

Namespaces isolate system resources so that each container has its own independent environment.

---

### What are cgroups?

Control Groups (cgroups) limit and monitor CPU, memory, and other resource usage for containers.

---

### What is OCI?

The Open Container Initiative (OCI) defines open standards for container images and runtimes, enabling interoperability across container platforms.

---

# Official References

- Docker Documentation
- Docker Engine Documentation
- Docker CLI Reference
- Docker Build Documentation
- Docker Compose Documentation
- OCI Image Specification
- OCI Runtime Specification

---

# Quick Revision

```text
Docker → Container Platform

Image → Read-only Template

Container → Running Image

Dockerfile → Image Blueprint

Docker Engine → Runtime

Docker Daemon → Background Service

Docker CLI → User Interface

Registry → Stores Images

Namespaces → Isolation

cgroups → Resource Control

OCI → Container Standards
```

---

# Skills Covered

✔ Docker Fundamentals

✔ Containerization

✔ Docker Architecture

✔ Docker Engine

✔ Docker Daemon

✔ Docker CLI

✔ Images

✔ Containers

✔ Registries

✔ OCI Standards

✔ Production Docker Workflow

---

# Status

🐳 Docker Fundamentals Completed 🚀
