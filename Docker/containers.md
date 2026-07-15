
# 🐳 Docker Containers

# Complete Docker Containers Guide for DevOps Engineers

> **Note:** This is a comprehensive starter edition designed as a single Markdown file for your repository.
> It follows Docker's official concepts and is structured for learning, revision, and interview preparation.

---

# Table of Contents

1. Introduction
2. Learning Objectives
3. What is a Docker Container?
4. Container vs Image
5. Container Architecture
6. Container Lifecycle
7. How Containers Work
8. Linux Namespaces
9. Linux cgroups
10. Writable Layer
11. PID 1
12. Container States
13. Essential Docker Commands
14. Restart Policies
15. Health Checks
16. Resource Limits
17. Logging
18. Security Best Practices
19. Production Best Practices
20. Troubleshooting
21. Hands-on Labs
22. Interview Questions
23. Official References
24. Quick Revision

---

# Introduction

A Docker container is a **running instance of a Docker image**. It packages an application together with its runtime, libraries, dependencies and configuration, allowing it to run consistently across environments.

Containers share the host operating system kernel while remaining isolated through Linux kernel features such as namespaces and cgroups.

---

# Learning Objectives

After completing this guide you will be able to:

- Understand Docker containers
- Explain container architecture
- Manage the container lifecycle
- Work with container commands
- Configure restart policies
- Configure health checks
- Limit CPU and memory
- Troubleshoot container issues
- Apply production best practices

---

# What is a Docker Container?

A container is an isolated execution environment created from a Docker image.

```text
Dockerfile
    ↓
Docker Image
    ↓
docker run
    ↓
Docker Container
```

Characteristics:

- Lightweight
- Portable
- Fast startup
- Isolated
- Ephemeral by default

---

# Container vs Image

| Docker Image | Docker Container |
|--------------|------------------|
| Read-only template | Running instance |
| Immutable | Writable layer |
| Stored locally/registry | Executes application |
| Created by docker build | Created by docker run |

---

# Container Architecture

```text
Developer
   ↓
Docker CLI
   ↓
Docker Daemon
   ↓
containerd
   ↓
runc
   ↓
Linux Kernel
   ↓
Running Container
```

---

# Container Lifecycle

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
Exited
      ↓
docker rm
      ↓
Deleted
```

---

# How Containers Work

When you execute:

```bash
docker run nginx
```

Docker:

1. Checks whether the image exists locally.
2. Pulls it from the registry if required.
3. Creates a writable layer.
4. Creates Linux namespaces.
5. Applies cgroup limits.
6. Configures networking.
7. Starts PID 1.
8. Returns the container ID.

---

# Linux Namespaces

Namespaces isolate:

- Processes (PID)
- Network
- Mounts
- IPC
- UTS (hostname)
- Users

Each container receives its own isolated view.

---

# Linux cgroups

cgroups control:

- CPU
- Memory
- Block I/O
- PIDs

Example:

```bash
docker run --memory=512m --cpus=1 nginx
```

---

# Writable Layer

Image layers remain read-only.

Containers receive one writable layer where runtime changes are stored.

Deleting the container removes that writable layer unless data is stored in volumes.

---

# PID 1

The first process inside a container is PID 1.

It is responsible for:

- Receiving signals
- Reaping child processes
- Determining container exit status

Production applications should handle SIGTERM correctly for graceful shutdown.

---

# Container States

- Created
- Running
- Paused
- Restarting
- Exited
- Dead

---

# Essential Docker Commands

## Create

```bash
docker create nginx
```

## Run

```bash
docker run -d --name web -p 8080:80 nginx
```

## List

```bash
docker ps
docker ps -a
```

## Start

```bash
docker start web
```

## Stop

```bash
docker stop web
```

## Restart

```bash
docker restart web
```

## Pause

```bash
docker pause web
docker unpause web
```

## Kill

```bash
docker kill web
```

## Remove

```bash
docker rm web
```

## Logs

```bash
docker logs web
docker logs -f web
```

## Execute Commands

```bash
docker exec -it web bash
```

## Inspect

```bash
docker inspect web
```

## Statistics

```bash
docker stats
```

## Running Processes

```bash
docker top web
```

## Copy Files

```bash
docker cp file.txt web:/tmp
docker cp web:/etc/nginx/nginx.conf .
```

---

# Restart Policies

Never:

```text
no
```

On failure:

```bash
docker run --restart=on-failure nginx
```

Always:

```bash
docker run --restart=always nginx
```

Unless stopped:

```bash
docker run --restart=unless-stopped nginx
```

---

# Health Checks

Example:

```dockerfile
HEALTHCHECK CMD curl -f http://localhost || exit 1
```

Check status:

```bash
docker inspect web
```

---

# Resource Limits

CPU

```bash
docker run --cpus=2 nginx
```

Memory

```bash
docker run --memory=1g nginx
```

PIDs

```bash
docker run --pids-limit=200 nginx
```

---

# Logging

View logs:

```bash
docker logs web
```

Follow:

```bash
docker logs -f web
```

Production recommendation:

- Centralize logs
- Rotate logs
- Avoid storing application logs only inside containers

---

# Security Best Practices

- Use official images
- Run as non-root
- Avoid privileged containers
- Keep images updated
- Use read-only filesystem where appropriate
- Scan images regularly
- Store secrets outside images
- Apply least privilege

---

# Production Best Practices

- Pin image versions
- Use health checks
- Configure restart policies
- Apply CPU and memory limits
- Use Docker volumes for persistent data
- Keep containers immutable
- Monitor resource usage
- Send logs to centralized logging

---

# Troubleshooting

## Container exits immediately

```bash
docker logs CONTAINER
```

## Cannot connect

```bash
docker inspect CONTAINER
```

Check:

- Ports
- Network
- Environment variables

## High CPU

```bash
docker stats
```

## High Disk Usage

```bash
docker system df
```

---

# Hands-on Labs

1. Run Nginx container.
2. Run Ubuntu interactively.
3. View logs.
4. Execute shell using `docker exec`.
5. Configure restart policy.
6. Configure memory limits.
7. Inspect container metadata.
8. Monitor CPU and memory with `docker stats`.

---

# Interview Questions

1. What is a Docker container?
2. Difference between image and container?
3. What is PID 1?
4. What are namespaces?
5. What are cgroups?
6. Difference between `docker run` and `docker create`?
7. Difference between `docker exec` and `docker attach`?
8. What happens during `docker stop`?
9. Why use restart policies?
10. How do you troubleshoot a restarting container?

---

# Official References

- Docker Engine Documentation
- Docker CLI Reference
- Docker Container Runtime Documentation
- OCI Runtime Specification
- Docker Best Practices

---

# Quick Revision

```text
Container → Running Image

docker run → Create + Start

docker create → Create Only

docker start → Start Existing

docker exec → Execute Command

docker logs → View Logs

docker inspect → Metadata

docker stats → Resource Usage

Namespaces → Isolation

cgroups → Resource Limits

PID 1 → Main Process
```

---

# Status

✅ Docker Containers Guide Completed
