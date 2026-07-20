# 📦 Docker Volumes

# Complete Docker Volumes Guide for DevOps Engineers

## Introduction
Docker volumes provide persistent storage for containers. Unlike a container's writable layer, a volume continues to exist even after the container is removed.

## Learning Objectives
- Understand Docker volumes
- Create and manage volumes
- Persist application data
- Share data between containers
- Backup and restore volumes

## What is a Docker Volume?
A Docker volume is Docker-managed storage designed for persistent data.

### Benefits
- Persistent storage
- Better performance
- Easy backup
- Container independent
- Production ready

## Types of Storage

| Type | Best For |
|------|----------|
| Volume | Production |
| Bind Mount | Development |
| tmpfs | Temporary memory storage |

## Volume Lifecycle

docker volume create → Attach to container → Read/Write → Container removed → Data persists

## Common Commands

```bash
docker volume create mydata
docker volume ls
docker volume inspect mydata
docker run -d -v mydata:/data nginx
docker volume rm mydata
docker volume prune
```

## Named vs Anonymous Volumes

Named volumes are reusable and recommended.
Anonymous volumes are auto-generated and mainly temporary.

## Bind Mount vs Volume

Volumes are Docker-managed and portable.
Bind mounts use host directories and are useful for development.

Example:

```bash
docker run -v $(pwd):/app nginx
```

## Backup

```bash
docker run --rm -v mydata:/data -v $(pwd):/backup ubuntu tar czf /backup/data.tar.gz /data
```

## Restore

```bash
docker run --rm -v mydata:/data -v $(pwd):/backup ubuntu tar xzf /backup/data.tar.gz -C /
```

## Production Best Practices

- Use named volumes
- Backup regularly
- Monitor disk usage
- Encrypt sensitive data
- Apply least privilege

## Security

- Avoid exposing sensitive host paths
- Restrict permissions
- Keep backups secure

## Troubleshooting

```bash
docker inspect CONTAINER
docker system df -v
```

## Hands-on Labs

1. Create a volume.
2. Mount it into a container.
3. Write data.
4. Delete the container.
5. Start another container with the same volume.
6. Verify persistence.

## Interview Questions

- What is a Docker volume?
- Difference between bind mounts and volumes?
- What is docker volume prune?
- How do you back up a volume?
- Can multiple containers use one volume?

## Official References

- Docker Volumes Documentation
- Docker Storage Documentation
- Docker CLI Reference

## Quick Revision

```
Volume = Persistent Storage
docker volume create
docker volume ls
docker volume inspect
docker volume rm
docker volume prune
```

✅ Docker Volumes Guide Completed
