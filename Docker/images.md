# 🖼️ Docker Images

# Complete Docker Images Guide for DevOps Engineers

Docker Images are the foundation of Docker containers. Every container starts from an image, making images one of the most important concepts in Docker.

A Docker Image is a **read-only, immutable template** that contains everything required to run an application, including the application code, runtime, system libraries, dependencies, configuration files, and metadata.

Images make applications portable, consistent, and reproducible across different environments.

This guide follows the concepts described in the **official Docker Documentation** and the **Open Container Initiative (OCI) Image Specification**.

---

# 🎯 Learning Objectives

After completing this guide, you will understand:

- What Docker Images are
- Why Docker Images are needed
- Image Architecture
- Image Layers
- Layer Caching
- Image IDs
- Image Tags
- Image Manifest
- Image Digest
- OCI Image Format
- Base Images
- Scratch Images
- Official Images
- Image Lifecycle
- Production Image Workflow

---

# 📖 What is a Docker Image?

A Docker Image is a lightweight, immutable, read-only template used to create Docker Containers.

Think of an image as a blueprint.

Example:

```text
Blueprint

↓

House
```

Docker

```text
Docker Image

↓

Docker Container
```

The image never changes after it is built.

Containers are created from images.

---

# Real-Life Analogy

Imagine baking a cake.

Recipe

↓

Bake Cake

↓

Cake

Docker works similarly.

Dockerfile

↓

Docker Image

↓

Docker Container

The recipe (Dockerfile) creates the image.

The image creates containers.

---

# Why Do We Need Images?

Without Docker Images

```text
Install Ubuntu

↓

Install Python

↓

Install Flask

↓

Copy Application

↓

Configure Everything
```

Every server requires manual setup.

With Docker Images

```text
Docker Image

↓

docker run

↓

Application Ready
```

Benefits

✔ Consistency

✔ Portability

✔ Faster Deployment

✔ Version Control

✔ Easy Rollback

✔ Immutable Infrastructure

---

# Docker Image Architecture

A Docker Image is composed of multiple read-only layers.

```text
                Docker Image

                      │

        ┌─────────────┼─────────────┐

        │             │             │

     Application   Python Runtime   Ubuntu

                      │

                 Base Image
```

Each layer stores only the changes introduced at that step.

---

# Image Layers

Every significant instruction in a Dockerfile creates a new layer.

Example Dockerfile

```dockerfile
FROM ubuntu:24.04

RUN apt update

RUN apt install python3 -y

COPY app.py /app/

CMD ["python3","/app/app.py"]
```

Generated layers

```text
Layer 5

Application

------------

Layer 4

Python Installed

------------

Layer 3

apt update

------------

Layer 2

Ubuntu Base

------------

Layer 1

Scratch
```

Each layer is immutable.

---

# Why Layers Matter

Layers provide major advantages.

Without layers

```text
Every Image

↓

Full Copy

↓

Huge Size
```

With layers

```text
Ubuntu Layer

↓

Shared

↓

Python Layer

↓

Shared

↓

Application Layer
```

Benefits

✔ Faster Downloads

✔ Smaller Images

✔ Shared Storage

✔ Faster Builds

---

# Immutable Images

Docker Images are immutable.

This means:

❌ Cannot modify an existing layer.

Instead

```text
Old Image

↓

Build Again

↓

New Image
```

This approach improves consistency and repeatability.

---

# Read-Only Layers

Image layers are read-only.

When a container starts

```text
Image Layers

↓

Writable Layer

↓

Running Container
```

Only the top writable layer changes.

Everything underneath remains unchanged.

---

# Writable Container Layer

Containers receive one writable layer.

Example

```text
Docker Image

↓

Container

↓

Create File

↓

Writable Layer Updated
```

When the container is deleted

```text
Writable Layer

↓

Deleted
```

The original image remains unchanged.

---

# Union File System

Docker combines multiple layers into one filesystem using a storage driver (commonly OverlayFS on modern Linux systems).

Example

```text
Application Layer

↓

Python Layer

↓

Ubuntu Layer

↓

Scratch Layer
```

Appears as

```text
/

bin

etc

usr

home

app
```

Applications see a single unified filesystem.

---

# Image Lifecycle

```text
Dockerfile

↓

docker build

↓

Docker Image

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
```

---

# Image ID

Every Docker Image has a unique identifier.

Example

```text
sha256:8d7d0f...
```

Display image IDs

```bash
docker images
```

Example output

```text
REPOSITORY    TAG       IMAGE ID

nginx         latest    605c77e624dd
```

---

# Image Tag

A tag identifies a specific version of an image.

Example

```text
nginx:1.27

ubuntu:24.04

python:3.12
```

General format

```text
repository:tag
```

If no tag is specified

Docker uses

```text
latest
```

> **Best Practice:** Use explicit version tags in production instead of relying on `latest`.

---

# Official Images

Official Images are maintained and published through the Docker Official Images program.

Examples

```text
ubuntu

nginx

mysql

redis

postgres

node

python
```

Advantages

✔ Well Maintained

✔ Trusted Sources

✔ Security Updates

✔ Comprehensive Documentation

---

# Base Images

A Base Image is the starting point for building another image.

Examples

```text
ubuntu

debian

alpine

rockylinux
```

Example Dockerfile

```dockerfile
FROM ubuntu:24.04
```

Everything else is built on top of this image.

---

# Scratch Image

`scratch` is a special empty base image.

Example

```dockerfile
FROM scratch
```

Used for:

- Static Go applications
- Minimal containers
- Security-focused deployments

There is no operating system or package manager inside a scratch image.

---

# Docker Hub

Docker Hub is the default public image registry.

Workflow

```text
docker pull nginx

↓

Docker Hub

↓

Image Downloaded

↓

Run Container
```

Popular repositories

- nginx
- ubuntu
- mysql
- redis
- node
- python

---

# OCI Image Specification

Docker Images follow the Open Container Initiative (OCI) Image Specification.

The specification defines:

- Image layout
- Image configuration
- Layer format
- Image manifest
- Metadata

This allows images to be used by compatible runtimes beyond Docker.

---

# Image Manifest

Every image contains a manifest.

The manifest describes:

- Image layers
- Platform
- Configuration
- Digest

Example

```text
Image

↓

Manifest

↓

Layer List

↓

Configuration

↓

Metadata
```

The runtime uses the manifest to assemble the image correctly.

---

# Image Digest

Every image also has a content-addressable digest.

Example

```text
sha256:2efb...

```

Unlike tags, a digest uniquely identifies the exact image content.

Benefits

✔ Integrity

✔ Reproducibility

✔ Supply Chain Security

---

# Pull Workflow

When you execute:

```bash
docker pull nginx
```

Docker performs these steps:

```text
Check Local Image

↓

Contact Registry

↓

Download Manifest

↓

Download Missing Layers

↓

Verify Digest

↓

Store Image Locally
```

Only layers that are not already present are downloaded.

---

# Image Storage

List local images

```bash
docker images
```

Detailed information

```bash
docker image ls
```

Inspect an image

```bash
docker image inspect nginx
```

---

# Best Practices

✔ Use official images whenever possible

✔ Pin image versions

✔ Keep images small

✔ Remove unused images

✔ Avoid unnecessary packages

✔ Rebuild images regularly to include security updates

✔ Store images in a trusted registry

---

# Common Mistakes

❌ Using `latest` in production

❌ Building very large images

❌ Installing unnecessary software

❌ Embedding secrets inside images

❌ Ignoring image updates

---

# Quick Revision

```text
Docker Image → Read-only Template

Layer → Immutable Filesystem Layer

Container → Running Image

Image ID → Unique Identifier

Tag → Image Version

Digest → Content Hash

Manifest → Image Metadata

Base Image → Starting Layer

Scratch → Empty Base Image

Docker Hub → Default Registry
```

---

# Skills Covered

✔ Docker Images

✔ Image Architecture

✔ Layers

✔ Writable Layer

✔ Image Lifecycle

✔ Image Tags

✔ Image IDs

✔ Base Images

✔ Scratch Images

✔ OCI Image Specification

✔ Image Manifest

✔ Image Digest

---

# Status

🖼️ Docker Images (Part 1) Completed ✅

---

# Working with Docker Images

Docker provides a rich set of commands for managing images. Understanding these commands is essential for daily development, CI/CD pipelines, and production deployments.

---

# Docker Image Commands

| Command | Purpose |
|----------|---------|
| `docker pull` | Download an image |
| `docker images` | List local images |
| `docker image ls` | List local images (modern syntax) |
| `docker image inspect` | Display detailed image information |
| `docker history` | Show image layers |
| `docker tag` | Create another tag |
| `docker save` | Save image as archive |
| `docker load` | Load archived image |
| `docker export` | Export container filesystem |
| `docker import` | Create image from filesystem archive |
| `docker rmi` | Remove image |
| `docker image prune` | Remove unused images |

---

# docker pull

The `docker pull` command downloads an image from a registry.

Syntax

```bash
docker pull IMAGE_NAME
```

Example

```bash
docker pull nginx
```

Specific version

```bash
docker pull nginx:1.27
```

Docker performs:

```text
Registry

↓

Manifest

↓

Layers

↓

Local Storage
```

Verify

```bash
docker images
```

---

# docker images

Displays all locally available images.

```bash
docker images
```

Example

```text
REPOSITORY    TAG       IMAGE ID       CREATED

ubuntu        24.04     xxxxxxx        2 weeks ago

nginx         1.27      yyyyyyy        5 days ago
```

Columns

Repository

Tag

Image ID

Created

Size

---

# docker image ls

Modern equivalent

```bash
docker image ls
```

Filter

```bash
docker image ls nginx
```

Display only dangling images

```bash
docker image ls -f dangling=true
```

---

# docker image inspect

Displays complete JSON metadata.

```bash
docker image inspect nginx
```

Useful information

- Image ID
- Environment Variables
- Labels
- Entrypoint
- Working Directory
- Architecture
- Operating System
- Layer Information

---

# docker history

Shows how an image was built.

```bash
docker history nginx
```

Example

```text
IMAGE

↓

Layer 1

↓

Layer 2

↓

Layer 3

↓

Layer 4
```

Useful for

- Image optimization
- Security review
- Layer analysis

---

# docker tag

Create another name for an image.

Example

```bash
docker tag nginx:1.27 my-nginx:v1
```

Result

```text
nginx:1.27

↓

my-nginx:v1
```

Both tags reference the same image until one is rebuilt.

---

# docker rmi

Remove an image.

```bash
docker rmi nginx
```

Remove by ID

```bash
docker rmi IMAGE_ID
```

Force removal

```bash
docker rmi -f IMAGE_ID
```

Docker cannot remove an image currently used by a running container.

---

# docker save

Save an image into a tar archive.

```bash
docker save nginx -o nginx.tar
```

Output

```text
nginx.tar
```

Use cases

- Offline transfer
- Air-gapped environments
- Backup

---

# docker load

Load a previously saved image.

```bash
docker load -i nginx.tar
```

Workflow

```text
docker save

↓

Transfer File

↓

docker load

↓

Image Restored
```

---

# docker export

Exports a **container filesystem**.

```bash
docker export CONTAINER_ID > container.tar
```

Important

This exports the container's filesystem **without image history or metadata**.

---

# docker import

Create a new image from an exported filesystem.

```bash
docker import container.tar myimage:v1
```

Use when rebuilding a filesystem into an image.

---

# Difference Between Save and Export

| docker save | docker export |
|--------------|---------------|
| Saves Image | Saves Container |
| Preserves Layers | No Layers |
| Preserves History | No History |
| Preserves Metadata | No Metadata |
| Use with `docker load` | Use with `docker import` |

---

# Docker Image Cache

Docker caches layers during image builds.

Example

```dockerfile
FROM ubuntu

RUN apt update

RUN apt install python3 -y

COPY app.py .

CMD ["python3","app.py"]
```

First build

```text
Build Layer 1

↓

Layer 2

↓

Layer 3

↓

Layer 4
```

Second build (only `app.py` changed)

```text
Reuse Layer 1

Reuse Layer 2

Reuse Layer 3

Build Layer 4
```

Benefits

✔ Faster builds

✔ Reduced CPU usage

✔ Less network traffic

---

# Layer Cache

Docker compares Dockerfile instructions.

If unchanged

↓

Reuse cached layer.

If changed

↓

Rebuild current layer and all following layers.

Example

```dockerfile
FROM ubuntu

RUN apt update

RUN apt install nginx

COPY website .
```

Changing `COPY`

Only rebuilds

```text
COPY

↓

Remaining Layers
```

Changing

```dockerfile
RUN apt update
```

Rebuilds

```text
RUN apt update

↓

RUN apt install

↓

COPY
```

---

# BuildKit

BuildKit is Docker's next-generation build engine.

Advantages

✔ Parallel Builds

✔ Better Layer Cache

✔ Secret Mounts

✔ SSH Forwarding

✔ Faster Builds

✔ Improved Performance

Check BuildKit

```bash
docker buildx version
```

---

# Build Cache Example

First Build

```text
Layer 1

↓

Layer 2

↓

Layer 3

↓

Layer 4
```

Second Build

```text
Cache Layer 1

↓

Cache Layer 2

↓

Build Layer 3

↓

Build Layer 4
```

---

# Multi-Platform Images

Docker supports multiple CPU architectures.

Examples

```text
linux/amd64

linux/arm64

linux/arm/v7
```

Inspect supported platforms

```bash
docker buildx imagetools inspect nginx:latest
```

Useful for

- Apple Silicon
- Raspberry Pi
- ARM Servers
- Cloud Platforms

---

# Dangling Images

Dangling images are untagged images that are no longer referenced.

View

```bash
docker image ls -f dangling=true
```

Remove

```bash
docker image prune
```

---

# Removing Unused Images

Remove unused images

```bash
docker image prune
```

Remove everything unused

```bash
docker system prune
```

Be careful in production because this can remove unused containers, networks, and build cache depending on the options used.

---

# Image Size Optimization

Bad

```dockerfile
FROM ubuntu

RUN apt update

RUN apt install python3

RUN apt install curl

RUN apt install git
```

Better

```dockerfile
FROM ubuntu

RUN apt update && \
    apt install -y python3 curl git && \
    rm -rf /var/lib/apt/lists/*
```

Advantages

✔ Fewer Layers

✔ Smaller Image

✔ Faster Build

---

# Production Workflow

```text
Developer

↓

Dockerfile

↓

docker build

↓

Docker Image

↓

Security Scan

↓

Docker Registry

↓

Production Server

↓

docker pull

↓

Container Running
```

---

# Best Practices

✔ Pin image versions

✔ Keep images small

✔ Remove unnecessary packages

✔ Combine related RUN instructions where appropriate

✔ Use BuildKit

✔ Clean package manager caches

✔ Remove unused images regularly

✔ Store images in trusted registries

---

# Common Mistakes

❌ Using `latest` everywhere

❌ Large base images

❌ Ignoring build cache

❌ Not cleaning package cache

❌ Too many image layers

---

# Interview Questions

### What is image caching?

Docker stores previously built layers and reuses them if the corresponding Dockerfile instruction and its inputs have not changed.

---

### Difference between docker save and docker export?

`docker save` exports an image with its layers and metadata.

`docker export` exports only a container filesystem.

---

### Why is BuildKit better?

BuildKit improves build speed, caching, secret handling, and supports advanced build features like parallel execution.

---

### What are dangling images?

Images without tags that are no longer referenced by any tagged image.

---

# Quick Revision

```text
docker pull → Download Image

docker images → List Images

docker inspect → Image Details

docker history → Layer History

docker save → Backup Image

docker load → Restore Image

docker export → Export Container

docker import → Import Filesystem

docker tag → New Tag

docker rmi → Remove Image

BuildKit → Faster Builds

Layer Cache → Reuse Existing Layers
```

---

# Status

🖼️ Docker Images (Part 2) Completed ✅

---

# Production Image Optimization

Building Docker images for development is easy.

Building Docker images for **production** requires:

- Smaller Images
- Faster Builds
- Better Security
- Lower Attack Surface
- Faster Deployment
- Better Resource Utilization

---

# Why Optimize Docker Images?

Large Docker Images cause:

❌ Slow Builds

❌ Slow Downloads

❌ Higher Storage Costs

❌ More Security Vulnerabilities

❌ Longer CI/CD Pipelines

Example

```text
2.5 GB Image

↓

Pull Time

5 Minutes
```

Optimized

```text
180 MB Image

↓

Pull Time

20 Seconds
```

---

# Multi-stage Builds

One of Docker's most important features.

Instead of shipping build tools inside the final image:

Builder Image

↓

Compile Application

↓

Copy Only Binary

↓

Production Image

---

## Without Multi-stage Build

```dockerfile
FROM golang:1.24

WORKDIR /app

COPY . .

RUN go build -o app

CMD ["./app"]
```

Image Contains

- Go Compiler
- Source Code
- Build Cache
- Binary

Large Image

---

## With Multi-stage Build

```dockerfile
FROM golang:1.24 AS builder

WORKDIR /app

COPY . .

RUN go build -o app

FROM alpine:3.21

COPY --from=builder /app/app .

CMD ["./app"]
```

Final Image Contains

✔ Binary Only

Result

Smaller

Faster

More Secure

---

# Multi-stage Build Workflow

```text
Builder Stage

↓

Install Dependencies

↓

Compile

↓

Create Binary

↓

Production Stage

↓

Copy Binary

↓

Run Application
```

---

# Distroless Images

Distroless Images contain only:

- Application
- Runtime Libraries

No

- Shell
- Package Manager
- apt
- yum
- bash

Example

```dockerfile
FROM gcr.io/distroless/static
```

Advantages

✔ Very Small

✔ Highly Secure

✔ Minimal Attack Surface

Suitable for

- Go
- Java
- Node.js
- Python (selected workloads)

---

# Alpine Linux Images

Example

```dockerfile
FROM alpine:3.21
```

Advantages

✔ Small

✔ Fast Download

✔ Low Memory

Disadvantages

- Some libraries unavailable
- Debugging harder
- musl libc instead of glibc

---

# Ubuntu Images

Example

```dockerfile
FROM ubuntu:24.04
```

Advantages

✔ Large package repository

✔ Easy debugging

✔ Familiar environment

Disadvantages

- Larger image size

---

# Debian Images

Example

```dockerfile
FROM debian:12-slim
```

Advantages

✔ Stable

✔ Good Compatibility

✔ Smaller than Ubuntu

Often preferred for production applications that need glibc compatibility.

---

# Image Comparison

| Image | Approximate Size | Use Case |
|---------|-----------------|----------|
| Scratch | Smallest | Static binaries |
| Distroless | Very Small | Secure production |
| Alpine | Small | Lightweight apps |
| Debian Slim | Medium | Production servers |
| Ubuntu | Larger | Development & compatibility |

---

# Choosing the Right Base Image

```text
Static Binary

↓

Scratch

-------------------

Secure Production

↓

Distroless

-------------------

Small Container

↓

Alpine

-------------------

General Production

↓

Debian Slim

-------------------

Development

↓

Ubuntu
```

---

# Image Security

Containers are only as secure as their images.

Security starts during image creation.

Best Practices

✔ Official Images

✔ Updated Images

✔ Minimal Images

✔ Scan Images

✔ Non-root User

✔ Remove Unused Packages

✔ Signed Images

---

# Image Vulnerabilities

Old Images

↓

Old Libraries

↓

Known CVEs

↓

Security Risk

Example

```text
Ubuntu

↓

Old OpenSSL

↓

Critical Vulnerability
```

Regularly rebuild images to include updated packages.

---

# Docker Scout

Docker Scout analyzes images for:

- Vulnerabilities
- Base Image Updates
- Security Recommendations
- Package Inventory

Benefits

✔ Continuous Security

✔ Dependency Analysis

✔ Recommendations

---

# Software Bill of Materials (SBOM)

An SBOM lists everything included inside an image.

Example

```text
Image

↓

Operating System

↓

Libraries

↓

Dependencies

↓

Application
```

Benefits

✔ Compliance

✔ Security

✔ Vulnerability Tracking

✔ Supply Chain Visibility

---

# Image Signing

How do we know an image wasn't modified?

Answer:

Digital Signatures.

Workflow

```text
Image

↓

Sign

↓

Registry

↓

Verify Signature

↓

Deploy
```

Benefits

✔ Integrity

✔ Authenticity

✔ Trusted Deployment

Concepts such as Docker Content Trust (legacy) and newer signing ecosystems (e.g., Sigstore/Cosign) are commonly used in supply chain security.

---

# Supply Chain Security

Modern image pipeline

```text
Developer

↓

GitHub

↓

CI Pipeline

↓

Build Image

↓

Security Scan

↓

Generate SBOM

↓

Sign Image

↓

Push Registry

↓

Deploy
```

Every stage improves trust.

---

# Running as Non-root

Avoid

```dockerfile
USER root
```

Better

```dockerfile
RUN adduser appuser

USER appuser
```

Benefits

✔ Reduced Privileges

✔ Better Security

✔ Production Best Practice

---

# Keep Images Small

Avoid

```dockerfile
RUN apt update

RUN apt install nginx

RUN apt install curl

RUN apt install vim
```

Better

```dockerfile
RUN apt update && \
apt install -y nginx curl && \
rm -rf /var/lib/apt/lists/*
```

Advantages

✔ Fewer Layers

✔ Smaller Image

---

# Use .dockerignore

Example

```text
.git

node_modules

logs

.env

*.log

README.md
```

Benefits

✔ Faster Build

✔ Smaller Context

✔ Better Security

---

# Pin Image Versions

Avoid

```dockerfile
FROM nginx:latest
```

Better

```dockerfile
FROM nginx:1.27
```

Benefits

✔ Predictable Deployments

✔ Stable Builds

✔ Easy Rollback

---

# Image Labels

Labels store metadata.

Example

```dockerfile
LABEL maintainer="Your Name"

LABEL version="1.0"

LABEL application="ERP"
```

Useful for

- Automation
- Inventory
- Documentation

---

# Production Build Pipeline

```text
Developer

↓

GitHub

↓

Pull Request

↓

CI Pipeline

↓

Docker Build

↓

Unit Tests

↓

Security Scan

↓

SBOM

↓

Image Signing

↓

Docker Registry

↓

Production
```

---

# Production Best Practices

✔ Use Official Images

✔ Keep Images Small

✔ Use Multi-stage Builds

✔ Scan Images Frequently

✔ Pin Versions

✔ Remove Build Dependencies

✔ Avoid Root User

✔ Add Health Checks

✔ Generate SBOM

✔ Sign Images

✔ Store Images in Trusted Registry

✔ Regularly Rebuild Images

---

# Common Production Mistakes

❌ Using latest tag

❌ Huge Images

❌ Installing unnecessary packages

❌ Keeping package cache

❌ Hardcoding passwords

❌ Running as root

❌ Ignoring image updates

❌ Ignoring vulnerability scans

---

# Troubleshooting

## Image Too Large

Check

```bash
docker history IMAGE_NAME
```

Look for

- Large Layers

- Unnecessary Packages

- Build Files

---

## Too Many Layers

Inspect

```bash
docker history IMAGE_NAME
```

Combine RUN instructions where appropriate.

---

## Slow Pull

Possible Causes

- Large Image

- Slow Network

- Registry Issues

Solution

- Smaller Base Image

- Multi-stage Build

- Layer Optimization

---

## Security Vulnerabilities

Actions

- Update Base Image

- Rebuild Image

- Scan Image

- Remove Unused Packages

---

# Production Architecture

```text
Developer

↓

GitHub

↓

GitHub Actions

↓

Docker Build

↓

Multi-stage Build

↓

Docker Scout

↓

SBOM

↓

Image Signing

↓

Amazon ECR

↓

Kubernetes

↓

Production
```

---

# Interview Questions

### Why should we use Multi-stage Builds?

To separate build dependencies from the runtime image, producing smaller and more secure production images.

---

### Why should we avoid latest?

Because it changes over time and can introduce unexpected behavior. Version-pinned images provide reproducible builds.

---

### What is Distroless?

A minimal image containing only the application and required runtime libraries, reducing attack surface.

---

### Why use Alpine?

To reduce image size and improve download speed, while understanding compatibility trade-offs.

---

### What is SBOM?

A Software Bill of Materials that lists all software components included in an image.

---

### What is Image Signing?

A mechanism to verify that an image has not been tampered with and comes from a trusted publisher.

---

# Quick Revision

```text
Multi-stage → Smaller Images

Distroless → Maximum Security

Alpine → Lightweight

Ubuntu → Easy Development

Debian Slim → Production Balance

SBOM → Software Inventory

Docker Scout → Security Analysis

Image Signing → Integrity

.dockerignore → Smaller Build Context

Non-root User → Better Security
```

---

# Skills Covered

✔ Multi-stage Builds

✔ Distroless Images

✔ Alpine Linux

✔ Debian Slim

✔ Image Security

✔ Docker Scout

✔ SBOM

✔ Image Signing

✔ Supply Chain Security

✔ Production Optimization

✔ Best Practices

---

# Status

🖼️ Docker Images (Part 3) Completed ✅

---

# 🧪 Hands-on Labs

The following labs will help you practice Docker Images from basic to advanced concepts.

---

# Lab 1 – Pull Your First Image

## Objective

Learn how to download images from Docker Hub.

Commands

```bash
docker pull nginx
```

Verify

```bash
docker images
```

Expected Output

```text
REPOSITORY   TAG     IMAGE ID

nginx        latest  xxxxxxxxx
```

---

# Lab 2 – Pull Specific Version

```bash
docker pull ubuntu:24.04
```

Verify

```bash
docker images
```

Observe

- Repository
- Tag
- Image ID
- Size

---

# Lab 3 – Compare Image Sizes

Download

```bash
docker pull ubuntu:24.04

docker pull alpine:3.21

docker pull debian:12-slim
```

Compare

```bash
docker images
```

Observe

- Image Size
- Download Time
- Storage Used

---

# Lab 4 – Inspect an Image

```bash
docker image inspect nginx
```

Look for

- Environment Variables

- Entrypoint

- Architecture

- Operating System

- Labels

---

# Lab 5 – View Image Layers

```bash
docker history nginx
```

Observe

- Layer Order

- Commands

- Layer Size

---

# Lab 6 – Tag an Image

```bash
docker tag nginx:1.27 my-nginx:v1
```

Verify

```bash
docker images
```

---

# Lab 7 – Save an Image

```bash
docker save nginx -o nginx.tar
```

Verify

```bash
ls
```

---

# Lab 8 – Load an Image

```bash
docker load -i nginx.tar
```

Verify

```bash
docker images
```

---

# Lab 9 – Remove Images

```bash
docker rmi my-nginx:v1
```

Remove dangling images

```bash
docker image prune
```

---

# Lab 10 – Build Your First Image

Dockerfile

```dockerfile
FROM nginx:1.27

COPY index.html /usr/share/nginx/html
```

Build

```bash
docker build -t website:v1 .
```

Verify

```bash
docker images
```

---

# 🚀 Production Projects

---

## Project 1

### Company Website

```text
Developer

↓

Dockerfile

↓

Docker Image

↓

Docker Hub

↓

Production Server
```

---

## Project 2

### Python Flask Application

```text
Flask

↓

Docker Image

↓

Docker Hub

↓

AWS EC2

↓

Running Container
```

---

## Project 3

### MERN Stack

```text
React

↓

Node.js

↓

MongoDB

↓

Docker Compose
```

---

## Project 4

### WordPress

```text
WordPress

↓

MySQL

↓

Docker Compose
```

---

## Project 5

### CI/CD Pipeline

```text
GitHub

↓

GitHub Actions

↓

Docker Build

↓

Security Scan

↓

Amazon ECR

↓

Amazon EKS
```

---

# 📸 Screenshot Guide

```text
screenshots/

images/

├── 01-docker-pull.png
├── 02-list-images.png
├── 03-image-inspect.png
├── 04-image-history.png
├── 05-image-tag.png
├── 06-image-save.png
├── 07-image-load.png
├── 08-image-prune.png
├── 09-build-image.png
├── 10-final-image.png
└── images-complete-lab.png
```

---

# 💼 Real Production Workflow

```text
Developer

↓

Git Repository

↓

Pull Request

↓

GitHub Actions

↓

Docker Build

↓

Unit Testing

↓

Image Scan

↓

SBOM Generation

↓

Image Signing

↓

Amazon ECR

↓

Amazon EKS

↓

Production
```

---

# 📖 Best Practices Checklist

| Practice | Status |
|----------|--------|
| Use Official Images | ⬜ |
| Pin Image Versions | ⬜ |
| Use Multi-stage Builds | ⬜ |
| Use Non-root User | ⬜ |
| Keep Images Small | ⬜ |
| Scan Images | ⬜ |
| Generate SBOM | ⬜ |
| Sign Images | ⬜ |
| Remove Unused Packages | ⬜ |
| Use `.dockerignore` | ⬜ |
| Remove Build Cache | ⬜ |
| Use Trusted Registry | ⬜ |

---

# 🎯 Common Interview Questions

## Beginner

### What is a Docker Image?

A Docker Image is a read-only template used to create Docker Containers.

---

### What is the difference between an Image and a Container?

Image

- Read-only
- Template

Container

- Running instance of an Image
- Writable layer

---

### What is Docker Hub?

Docker Hub is Docker's default public registry used to store and distribute container images.

---

### What is a Base Image?

A Base Image is the starting image used to build another Docker image.

---

### What is Scratch?

A special empty base image used to create minimal containers.

---

## Intermediate

### What is Layer Caching?

Docker reuses previously built layers when the corresponding Dockerfile instructions and inputs have not changed.

---

### Why are Docker Images immutable?

Immutability ensures consistent, repeatable deployments by preventing modification of existing image layers.

---

### Difference between Image ID and Image Tag?

Image ID

- Unique identifier
- Generated automatically

Image Tag

- Human-readable version label
- Can be changed

---

### Difference between docker save and docker export?

docker save

- Image
- Preserves layers
- Preserves metadata

docker export

- Container filesystem only
- No layer history

---

### What is Image Manifest?

Metadata describing the image configuration and layers.

---

## Advanced

### What is OCI Image Specification?

A standard defining how container images are structured and distributed.

---

### What is Image Digest?

A SHA-256 hash uniquely identifying image content.

---

### Why are Multi-stage Builds important?

They separate build dependencies from runtime artifacts, resulting in smaller and more secure images.

---

### What is SBOM?

Software Bill of Materials.

Lists every package and dependency inside an image.

---

### What is Docker Scout?

A Docker tool used to analyze images for vulnerabilities and provide recommendations.

---

### Why should production avoid latest?

Because `latest` is mutable and may point to different image versions over time.

---

## Scenario-Based Questions

### Your Docker image is 2 GB. How would you reduce its size?

Expected discussion:

- Multi-stage Builds
- Smaller Base Image
- Remove unnecessary packages
- Combine RUN commands
- Clean package caches
- Use `.dockerignore`

---

### A security scan reports critical vulnerabilities in your image. What steps would you take?

Expected discussion:

- Update the base image
- Rebuild the image
- Remove unnecessary software
- Scan again
- Redeploy with the updated image

---

### Developers report slow CI builds due to Docker images. How would you optimize them?

Expected discussion:

- Improve Dockerfile layer ordering
- Use BuildKit
- Reuse build cache
- Optimize the build context
- Use smaller base images

---

# 📚 Official Documentation

Study the following resources for the latest guidance:

- Docker Engine Documentation
- Docker Images Documentation
- Docker CLI Reference
- Docker Build Documentation
- Docker BuildKit Documentation
- Docker Scout Documentation
- Docker Hub Documentation
- OCI Image Specification
- OCI Runtime Specification

---

# ⚡ One-Page Revision

```text
Docker Image

↓

Read-only Template

↓

Image Layers

↓

Immutable

↓

docker build

↓

Docker Image

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

--------------------------------

Image ID → Unique Identifier

Tag → Version

Digest → SHA-256

Manifest → Metadata

Base Image → Starting Point

Scratch → Empty Image

BuildKit → Faster Builds

SBOM → Software Inventory

Docker Scout → Security Analysis
```

---

# 🧠 Skills Covered

✔ Docker Images

✔ OCI Image Specification

✔ Layer Architecture

✔ Image Manifest

✔ Image Digest

✔ Image Lifecycle

✔ Image Commands

✔ BuildKit

✔ Layer Cache

✔ Multi-stage Builds

✔ Distroless Images

✔ Docker Scout

✔ SBOM

✔ Image Signing

✔ Image Optimization

✔ Production Best Practices

✔ Troubleshooting

✔ Hands-on Labs

✔ Interview Preparation

---

# 🔗 Related Topics

- Docker Architecture
- Docker Containers
- Dockerfile
- Docker Networks
- Docker Volumes
- Docker Compose
- Docker Registries
- Docker Security

---

# 🎉 Congratulations!

You have completed the **Docker Images** module.

You now understand:

- How Docker Images are built
- How Docker stores layers
- How images are distributed
- How to optimize production images
- How to secure images
- How images are used in CI/CD pipelines
- Docker image best practices based on official guidance

---

# Status

✅ Docker Images Completed Successfully 🚀
