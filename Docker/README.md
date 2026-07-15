# 🐳 Docker

# Complete Docker Guide for DevOps Engineers

Docker is an open-source containerization platform that allows developers and DevOps engineers to build, package, distribute, and run applications consistently across different environments.

Instead of worrying about whether an application works on one machine but not another, Docker packages the application together with its dependencies, libraries, runtime, and configuration into a lightweight unit called a **container**.

Docker has become one of the most important tools in modern DevOps because it enables faster development, easier deployment, better scalability, and consistent application environments.

---

# 🎯 Learning Objectives

After completing this section, you will be able to:

- Understand containerization
- Understand Docker architecture
- Install Docker
- Work with Docker Images
- Manage Containers
- Write Dockerfiles
- Use Docker Compose
- Manage Docker Networks
- Manage Docker Volumes
- Build Multi-Container Applications
- Optimize Docker Images
- Secure Docker Containers
- Deploy production-ready applications

---

# 📖 What is Docker?

Docker is a containerization platform that packages an application and all its dependencies into a standardized unit called a **container**.

A container includes:

- Application Code
- Runtime
- Libraries
- Dependencies
- System Tools
- Configuration Files

Example:

```text
Application

↓

Docker Image

↓

Docker Container

↓

Runs Anywhere
```

This ensures the application behaves the same way regardless of where it is deployed.

---

# Why Do We Need Docker?

Imagine a developer builds an application on their laptop.

```text
Developer Laptop

↓

Works Perfectly
```

After deploying to a server:

```text
Production Server

↓

Application Fails
```

Reasons may include:

- Different OS versions
- Missing libraries
- Different runtime versions
- Configuration differences

This problem is commonly summarized as:

> "It works on my machine."

Docker solves this by packaging everything the application needs.

```text
Application

↓

Docker Image

↓

Container

↓

Runs the Same Everywhere
```

Benefits

✔ Consistent Environment

✔ Fast Deployment

✔ Isolation

✔ Portability

✔ Scalability

✔ Easy Rollback

---

# What is a Container?

A container is a lightweight, isolated runtime environment that shares the host operating system kernel while packaging an application with everything it needs to run.

Container contains:

```text
Application

Libraries

Runtime

Dependencies

Configuration
```

Containers are:

- Lightweight
- Fast
- Portable
- Isolated

---

# What is Containerization?

Containerization is the process of packaging an application together with its dependencies into a container.

Example

```text
Application

↓

Container

↓

Runs on

Laptop

Server

Cloud

Kubernetes
```

---

# Why Containers Instead of Virtual Machines?

Traditional deployment

```text
Application

↓

Operating System

↓

Hardware
```

Virtualization

```text
Application

↓

Guest OS

↓

Hypervisor

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

Containers do not require a full guest operating system, making them much lighter.

---

# Virtual Machine vs Docker

| Feature | Virtual Machine | Docker Container |
|----------|-----------------|------------------|
| Guest OS | Required | Not Required |
| Startup Time | Minutes | Seconds |
| Resource Usage | High | Low |
| Size | GBs | MBs |
| Performance | Lower | Higher |
| Portability | Limited | Excellent |
| Isolation | Strong | Process-level |

---

# Docker Architecture

```text
                Developer

                     │

               Docker CLI

                     │

               Docker Engine

        ┌────────────┼────────────┐

        │            │            │

     Images      Containers     Networks

        │            │            │

        └────────────┼────────────┘

                     │

              Host Operating System

                     │

                  Hardware
```

---

# Docker Components

Docker consists of several components.

```text
Docker

│

├── Docker Client

├── Docker Engine

├── Docker Daemon

├── Docker Images

├── Docker Containers

├── Docker Networks

├── Docker Volumes

└── Docker Registry
```

---

# Docker Client

The Docker Client is the command-line interface (CLI) used to interact with Docker.

Example:

```bash
docker run nginx
```

The CLI sends requests to the Docker Daemon.

---

# Docker Daemon

The Docker Daemon (`dockerd`) is the background service responsible for:

- Building images
- Running containers
- Managing networks
- Managing volumes
- Pulling images
- Communicating with registries

---

# Docker Engine

Docker Engine includes:

- Docker Daemon
- Docker CLI
- Docker REST API

It is the core runtime that powers Docker.

---

# Docker Images

A Docker Image is a read-only template used to create containers.

Examples:

- nginx
- ubuntu
- mysql
- redis
- node
- python

Images are built from Dockerfiles.

---

# Docker Containers

A container is a running instance of an image.

Example

```text
Docker Image

↓

docker run

↓

Running Container
```

---

# Docker Registry

A registry stores Docker Images.

Examples:

- Docker Hub
- Amazon ECR
- GitHub Container Registry
- Azure Container Registry

---

# Docker Workflow

```text
Write Dockerfile

↓

Build Image

↓

Run Container

↓

Test Application

↓

Push Image

↓

Deploy
```

---

# Docker Image Lifecycle

```text
Dockerfile

↓

docker build

↓

Docker Image

↓

docker push

↓

Docker Registry

↓

docker pull

↓

docker run

↓

Container
```

---

# Docker in DevOps

Docker is commonly used for:

✔ Application Packaging

✔ CI/CD Pipelines

✔ Microservices

✔ Kubernetes

✔ Testing

✔ Cloud Deployments

✔ Local Development

---

# Real Production Architecture

```text
               Developer

                    │

                GitHub

                    │

             GitHub Actions

                    │

             Build Docker Image

                    │

              Docker Registry

                    │

             Kubernetes Cluster

        ┌────────────┼────────────┐

        │            │            │

   Container    Container    Container

                    │

            Application Users
```

---

# Benefits of Docker

✔ Faster Deployment

✔ Lightweight

✔ Portable

✔ Consistent Environment

✔ Easy Scaling

✔ Better Resource Utilization

✔ Version Control for Images

✔ Easy Rollback

✔ Simplified CI/CD

✔ Cloud Native

---

# Common Use Cases

Docker is widely used for:

- Web Applications
- REST APIs
- Microservices
- Machine Learning Applications
- Databases
- CI/CD Pipelines
- Kubernetes Deployments
- Development Environments

---

# Best Practices

✔ Use official base images

✔ Keep images small

✔ Use multi-stage builds

✔ Avoid running containers as root

✔ Use `.dockerignore`

✔ Pin image versions instead of relying on `latest`

✔ Store secrets securely

✔ Scan images for vulnerabilities

✔ Use health checks

✔ Monitor container logs

---

# Docker Ecosystem

```text
Docker

│

├── Docker Hub

├── Docker Desktop

├── Docker Engine

├── Docker Compose

├── BuildKit

├── Docker Scout

└── Docker Extensions
```

---

# Learning Path

```text
03-Docker/

│

├── README

├── Docker

├── Installation

├── Docker Architecture

├── Images

├── Containers

├── Dockerfile

├── Volumes

├── Bind Mounts

├── Networks

├── Docker Compose

├── Registries

├── Docker Hub

├── Environment Variables

├── Logs

├── Inspect

├── Exec

├── Build

├── Push & Pull

├── Security

├── Optimization

├── Projects

├── Practice Lab

└── Screenshots
```

---

# Projects Included

## Project 1

Containerize a Python Flask Application

---

## Project 2

Containerize a Node.js Application

---

## Project 3

Deploy WordPress with MySQL using Docker Compose

---

## Project 4

Deploy a Three-Tier Application

---

## Project 5

Deploy a Production Multi-Container Application

---

# Official References

- Docker Documentation
- Docker Engine Documentation
- Docker CLI Reference
- Docker Compose Documentation
- Docker Build Documentation
- Docker Hub Documentation
- OCI (Open Container Initiative) Specifications

---

# Skills You Will Gain

✔ Docker Fundamentals

✔ Containerization

✔ Docker Images

✔ Docker Containers

✔ Docker Engine

✔ Docker Architecture

✔ Docker Registry

✔ Docker Workflow

✔ DevOps Integration

✔ Production Deployments

---

# Repository Structure

```text
03-Docker/

├── README.md
├── docker.md
├── installation.md
├── docker-architecture.md
├── images.md
├── containers.md
├── dockerfile.md
├── volumes.md
├── bind-mounts.md
├── networks.md
├── docker-compose.md
├── registries.md
├── dockerhub.md
├── environment-variables.md
├── logs.md
├── inspect.md
├── exec.md
├── build.md
├── push-pull.md
├── security.md
├── optimization.md
├── projects.md
├── practice-lab.md
└── screenshots/
```

---

# Status

🐳 Docker Section Started 🚀
