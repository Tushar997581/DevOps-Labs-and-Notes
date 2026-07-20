# 📂 Docker Bind Mounts

# Complete Docker Bind Mounts Guide for DevOps Engineers

## Introduction

A **Bind Mount** maps a file or directory from the **host machine** directly into a Docker container. Unlike Docker volumes, the host manages the storage.

---

## Learning Objectives

- Understand bind mounts
- Mount host files and directories
- Compare bind mounts and volumes
- Use read-only mounts
- Follow production best practices

---

# What is a Bind Mount?

A bind mount gives a container direct access to a specific path on the host.

```text
Host Directory
      │
      ▼
Bind Mount
      │
      ▼
Container Directory
```

Changes made on either side are immediately visible to the other.

---

# Why Use Bind Mounts?

- Local development
- Live code editing
- Sharing configuration files
- Testing applications
- Accessing host logs

---

# Basic Syntax

```bash
docker run -v /host/path:/container/path nginx
```

Recommended modern syntax:

```bash
docker run --mount type=bind,source=/host/path,target=/container/path nginx
```

---

# Examples

## Mount Current Directory

```bash
docker run -it -v $(pwd):/app ubuntu
```

## Mount Configuration File

```bash
docker run -d \
-v /etc/nginx/nginx.conf:/etc/nginx/nginx.conf \
nginx
```

## Read-only Mount

```bash
docker run \
-v $(pwd):/app:ro \
nginx
```

---

# Bind Mount vs Volume

| Feature | Bind Mount | Volume |
|---------|------------|--------|
| Managed By | Host | Docker |
| Portability | Lower | Higher |
| Best For | Development | Production |
| Performance | Good | Optimized |

---

# File vs Directory Mounts

Directory:

```bash
-v /home/user/project:/app
```

Single file:

```bash
-v /home/user/app.conf:/etc/app.conf
```

---

# Read-only Mounts

Prevent accidental modification of host files.

```bash
docker run --mount type=bind,source=$(pwd),target=/app,readonly nginx
```

---

# Common Use Cases

- Source code development
- Configuration management
- Log analysis
- Testing
- CI/CD pipelines

---

# Security Considerations

- Avoid mounting sensitive directories like `/`
- Prefer read-only mounts when possible
- Limit container privileges
- Validate host file permissions

---

# Troubleshooting

Check mounts:

```bash
docker inspect CONTAINER
```

Verify inside container:

```bash
docker exec -it CONTAINER ls /app
```

Permission issues:

```bash
chmod
chown
```

---

# Production Best Practices

- Use volumes for persistent application data
- Use bind mounts mainly for development
- Use read-only mounts for configuration
- Avoid exposing sensitive host paths
- Document mount locations

---

# Hands-on Labs

1. Mount a project directory.
2. Edit files on the host.
3. Verify changes inside the container.
4. Create a read-only bind mount.
5. Mount a configuration file.
6. Inspect mount information.

---

# Interview Questions

1. What is a bind mount?
2. Bind mount vs volume?
3. When should bind mounts be used?
4. What is a read-only mount?
5. How do you inspect mounted paths?
6. Can you mount a single file?
7. What are the security risks?

---

# Official References

- Docker Bind Mount Documentation
- Docker Storage Documentation
- Docker CLI Reference

---

# Quick Revision

```text
Bind Mount = Host Path

-v host:container

--mount type=bind

Read-only = :ro

Best For = Development

Volume = Production
```

---

✅ **Docker Bind Mounts Guide Completed**
