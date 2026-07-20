# 🐙 Docker Compose

# Complete Docker Compose Guide for DevOps Engineers

> Docker Compose is a tool for defining and running multi-container Docker applications using a single YAML file.

---

# Table of Contents

1. Introduction
2. Learning Objectives
3. What is Docker Compose?
4. Why Docker Compose?
5. Docker Compose Architecture
6. Docker Compose V2
7. docker-compose.yml Structure
8. Services
9. Networks
10. Volumes
11. Environment Variables
12. depends_on
13. Health Checks
14. Scaling Services
15. Common Commands
16. Production Best Practices
17. Troubleshooting
18. Hands-on Labs
19. Interview Questions
20. Official References
21. Quick Revision

---

# Introduction

Docker Compose simplifies the deployment of applications consisting of multiple containers.

Instead of running several `docker run` commands, all services are defined in a single YAML file.

```text
docker-compose.yml
        │
docker compose up
        │
Multiple Containers
```

---

# Learning Objectives

- Understand Docker Compose
- Build multi-container applications
- Configure services, networks, and volumes
- Use environment variables
- Scale services
- Apply production best practices

---

# What is Docker Compose?

Docker Compose is a tool that lets you define infrastructure for multi-container applications as code.

Example services:

- Web
- Database
- Redis
- Nginx
- Backend API

---

# Why Docker Compose?

Benefits:

- Infrastructure as Code
- Easy deployment
- Repeatable environments
- Service isolation
- Automatic networking

---

# Docker Compose Architecture

```text
docker-compose.yml
        │
Docker Compose CLI
        │
Docker Engine
        │
Containers
Networks
Volumes
```

---

# Docker Compose V2

Modern Docker uses:

```bash
docker compose
```

Older versions used:

```bash
docker-compose
```

Compose V2 is included with Docker Desktop and modern Docker Engine installations.

---

# docker-compose.yml Structure

Example:

```yaml
services:
  web:
    image: nginx

  db:
    image: mysql:8

volumes:

networks:
```

---

# Services

Each service defines one container.

Example:

```yaml
services:
  web:
    image: nginx
    ports:
      - "8080:80"
```

---

# Networks

Compose automatically creates a default network.

Custom example:

```yaml
networks:
  app-network:
```

Assign:

```yaml
services:
  web:
    networks:
      - app-network
```

---

# Volumes

Persistent storage:

```yaml
volumes:
  mysql-data:
```

Mount:

```yaml
services:
  db:
    volumes:
      - mysql-data:/var/lib/mysql
```

---

# Environment Variables

Inline:

```yaml
environment:
  APP_ENV: production
```

Using an `.env` file:

```yaml
environment:
  - DB_HOST=${DB_HOST}
```

---

# depends_on

Control startup order.

```yaml
services:
  web:
    depends_on:
      - db
```

Note: `depends_on` does not wait until the dependency is healthy.

---

# Health Checks

```yaml
healthcheck:
  test: ["CMD","curl","-f","http://localhost"]
  interval: 30s
  timeout: 10s
  retries: 3
```

---

# Scaling Services

Scale a service:

```bash
docker compose up --scale web=3
```

---

# Common Commands

Start:

```bash
docker compose up
```

Detached:

```bash
docker compose up -d
```

Stop:

```bash
docker compose down
```

View logs:

```bash
docker compose logs
```

Restart:

```bash
docker compose restart
```

Build:

```bash
docker compose build
```

List services:

```bash
docker compose ps
```

Execute:

```bash
docker compose exec web bash
```

---

# Production Best Practices

- Pin image versions
- Use named volumes
- Use custom networks
- Store secrets securely
- Keep configuration in `.env`
- Add health checks
- Monitor logs
- Use restart policies

---

# Troubleshooting

Validate configuration:

```bash
docker compose config
```

View logs:

```bash
docker compose logs
```

Check running services:

```bash
docker compose ps
```

---

# Hands-on Labs

1. Deploy Nginx + MySQL.
2. Build a Flask + Redis application.
3. Create custom networks.
4. Mount persistent volumes.
5. Use `.env` variables.
6. Scale the web service.
7. Add health checks.

---

# Interview Questions

1. What is Docker Compose?
2. Difference between Docker and Docker Compose?
3. What is a service?
4. What is docker-compose.yml?
5. What is depends_on?
6. How do services communicate?
7. Difference between compose up and compose down?
8. How do you scale services?
9. Why use volumes in Compose?
10. What is Docker Compose V2?

---

# Official References

- Docker Compose Documentation
- Compose File Reference
- Docker CLI Reference

---

# Quick Revision

```text
docker compose up

docker compose down

docker compose build

docker compose logs

docker compose exec

docker compose ps

Services

Networks

Volumes

depends_on

Health Checks
```

---

# Status

✅ Docker Compose Guide Completed
