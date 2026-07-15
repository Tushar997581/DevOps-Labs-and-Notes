
# 🐳 Dockerfile

# Complete Dockerfile Guide for DevOps Engineers

> This guide is based on Docker's official concepts and is designed for GitHub documentation, interview preparation, and production use.

---

# Table of Contents

1. Introduction
2. Learning Objectives
3. What is a Dockerfile?
4. Why Dockerfiles?
5. Docker Build Process
6. Dockerfile Instructions
7. CMD vs ENTRYPOINT
8. COPY vs ADD
9. ARG vs ENV
10. Build Context
11. .dockerignore
12. Build Cache
13. BuildKit
14. Multi-stage Builds
15. Image Optimization
16. Security Best Practices
17. Production Dockerfile
18. Common Mistakes
19. Troubleshooting
20. Hands-on Labs
21. Interview Questions
22. Official References
23. Quick Revision

---

# Introduction

A Dockerfile is a text file containing instructions that Docker uses to build an image.

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

# Learning Objectives

- Understand Dockerfiles
- Learn every common instruction
- Build production-ready images
- Optimize image size
- Use BuildKit
- Create multi-stage builds
- Apply security best practices

---

# Why Dockerfiles?

Benefits:

- Infrastructure as Code
- Repeatable builds
- Version control
- Automation
- Consistent deployments

---

# Docker Build Process

```text
Dockerfile
    ↓
Build Context
    ↓
Docker Engine
    ↓
Image Layers
    ↓
Docker Image
```

---

# Common Dockerfile Instructions

## FROM

Defines the base image.

```dockerfile
FROM ubuntu:24.04
```

---

## LABEL

Adds metadata.

```dockerfile
LABEL app="erp"
LABEL version="1.0"
```

---

## RUN

Executes commands during image build.

```dockerfile
RUN apt update && apt install -y nginx
```

---

## WORKDIR

Sets the working directory.

```dockerfile
WORKDIR /app
```

---

## COPY

Copies files from the build context.

```dockerfile
COPY . .
```

---

## ADD

Copies files and supports remote URLs and archive extraction.

```dockerfile
ADD app.tar.gz /app
```

Use COPY unless ADD's extra features are required.

---

## ENV

Defines environment variables.

```dockerfile
ENV APP_ENV=production
```

---

## ARG

Defines build-time variables.

```dockerfile
ARG VERSION=1.0
```

---

## EXPOSE

Documents the intended listening port.

```dockerfile
EXPOSE 80
```

---

## USER

Run the container as a non-root user.

```dockerfile
USER appuser
```

---

## VOLUME

Declares a mount point.

```dockerfile
VOLUME /data
```

---

## HEALTHCHECK

Defines a container health check.

```dockerfile
HEALTHCHECK CMD curl -f http://localhost || exit 1
```

---

## CMD

Default command executed when the container starts.

```dockerfile
CMD ["nginx","-g","daemon off;"]
```

---

## ENTRYPOINT

Defines the executable that always runs.

```dockerfile
ENTRYPOINT ["python3"]
```

---

# CMD vs ENTRYPOINT

| CMD | ENTRYPOINT |
|-----|------------|
| Default command | Default executable |
| Easily overridden | Typically remains fixed |

Often used together:

```dockerfile
ENTRYPOINT ["python3"]
CMD ["app.py"]
```

---

# COPY vs ADD

| COPY | ADD |
|------|-----|
| Copies files | Copies files, extracts local archives, supports remote URLs |
| Preferred | Use only when extra functionality is required |

---

# ARG vs ENV

| ARG | ENV |
|-----|-----|
| Build time | Runtime |
| Not persisted by default | Available in running container |

---

# Build Context

Everything in the build directory is sent to Docker.

Reduce build context using `.dockerignore`.

---

# .dockerignore

Example:

```text
.git
node_modules
*.log
.env
```

Benefits:

- Faster builds
- Smaller build context
- Better security

---

# Build Cache

Docker reuses unchanged layers.

Best practice:

- Copy dependency files first
- Install dependencies
- Copy application code last

---

# BuildKit

Advantages:

- Parallel builds
- Better caching
- Secret mounts
- Faster builds

Verify:

```bash
docker buildx version
```

---

# Multi-stage Builds

Example:

```dockerfile
FROM golang:1.24 AS builder
WORKDIR /src
COPY . .
RUN go build -o app

FROM alpine:3.21
COPY --from=builder /src/app /app
CMD ["/app"]
```

Benefits:

- Smaller images
- Better security
- No build tools in runtime image

---

# Image Optimization

- Use small base images
- Combine RUN commands
- Remove package cache
- Use multi-stage builds
- Avoid unnecessary packages
- Use .dockerignore

---

# Security Best Practices

- Use official images
- Pin versions
- Run as non-root
- Don't hardcode secrets
- Scan images
- Keep images updated

---

# Production Dockerfile Example

```dockerfile
FROM python:3.12-slim

WORKDIR /app

COPY requirements.txt .

RUN pip install --no-cache-dir -r requirements.txt

COPY . .

RUN useradd -m appuser
USER appuser

EXPOSE 8000

CMD ["python","app.py"]
```

---

# Common Mistakes

- Using latest tag
- Running as root
- Large images
- Ignoring .dockerignore
- Too many layers
- Hardcoded secrets

---

# Troubleshooting

Image too large

```bash
docker history IMAGE
```

Build fails

```bash
docker build .
```

Review the error near the failing instruction.

---

# Hands-on Labs

1. Create your first Dockerfile.
2. Build an Nginx image.
3. Containerize a Flask app.
4. Create a multi-stage build.
5. Use BuildKit.
6. Optimize image size.

---

# Interview Questions

1. What is a Dockerfile?
2. Difference between RUN and CMD?
3. CMD vs ENTRYPOINT?
4. COPY vs ADD?
5. ARG vs ENV?
6. What is BuildKit?
7. Why use multi-stage builds?
8. What is .dockerignore?
9. How do you optimize a Docker image?
10. Why avoid running as root?

---

# Official References

- Dockerfile Reference
- Docker Build Documentation
- Docker BuildKit Documentation
- Docker Best Practices
- OCI Image Specification

---

# Quick Revision

```text
FROM → Base Image

RUN → Build Commands

COPY → Copy Files

ADD → Copy + Extra Features

WORKDIR → Working Directory

ENV → Runtime Variables

ARG → Build Variables

CMD → Default Command

ENTRYPOINT → Executable

HEALTHCHECK → Health Probe

BuildKit → Faster Builds

Multi-stage → Smaller Images
```

---

# Status

✅ Dockerfile Guide Completed
