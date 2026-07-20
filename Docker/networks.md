# 🌐 Docker Networks

# Complete Docker Networks Guide for DevOps Engineers

> Docker networking enables communication between containers, the host system, and external networks. Understanding Docker networks is essential for building scalable, secure, and production-ready applications.

---

# Table of Contents

1. Introduction
2. Learning Objectives
3. What is Docker Networking?
4. Why Docker Networks?
5. Docker Network Architecture
6. Network Drivers
7. Bridge Network
8. Host Network
9. None Network
10. Overlay Network
11. Macvlan Network
12. Container Communication
13. DNS & Service Discovery
14. Port Publishing
15. Network Commands
16. Custom Networks
17. Network Security
18. Production Best Practices
19. Troubleshooting
20. Hands-on Labs
21. Interview Questions
22. Official References
23. Quick Revision

---

# Introduction

Docker creates isolated virtual networks that allow containers to communicate securely while remaining separated from each other and the host.

```text
Internet
    │
Host Machine
    │
Docker Engine
    │
Docker Network
    ├── Container A
    ├── Container B
    └── Container C
```

---

# Learning Objectives

- Understand Docker networking
- Learn network drivers
- Connect containers
- Publish container ports
- Create custom networks
- Troubleshoot networking issues

---

# What is Docker Networking?

Docker networking provides communication between:

- Container ↔ Container
- Container ↔ Host
- Container ↔ Internet
- Container ↔ External Services

---

# Why Docker Networks?

Benefits:

- Isolation
- Security
- Service Discovery
- Scalability
- Load Distribution

---

# Docker Network Architecture

```text
Application
      │
Container
      │
Virtual Network Interface
      │
Docker Network Driver
      │
Linux Networking Stack
      │
Physical Network
```

---

# Network Drivers

| Driver | Use Case |
|---------|----------|
| bridge | Default for standalone containers |
| host | Shares host networking |
| none | No networking |
| overlay | Multi-host communication |
| macvlan | Assign MAC addresses to containers |

---

# Bridge Network

Default network for standalone containers.

Create custom bridge:

```bash
docker network create my-network
```

Run container:

```bash
docker run -d --network my-network nginx
```

---

# Host Network

Container shares the host network stack.

```bash
docker run --network host nginx
```

Advantages:
- High performance
- No NAT

Limitations:
- Reduced isolation
- Linux only

---

# None Network

No network interface except loopback.

```bash
docker run --network none alpine
```

---

# Overlay Network

Used with Docker Swarm to connect containers across multiple hosts.

```bash
docker network create \
--driver overlay app-network
```

---

# Macvlan Network

Assigns a unique MAC address and IP address from the physical network.

Useful when containers must appear as physical devices.

---

# Container Communication

Containers on the same custom network communicate using container names.

Example:

```bash
docker network create app-net

docker run -d --name web --network app-net nginx

docker run -it --network app-net busybox
```

---

# DNS & Service Discovery

Docker provides an internal DNS server for custom networks.

Example:

```text
web
database
redis
```

Containers can resolve each other by name.

---

# Port Publishing

Expose container ports:

```bash
docker run -p 8080:80 nginx
```

Format:

```text
HostPort:ContainerPort
```

Examples:

```bash
-p 3000:3000
-p 5432:5432
-p 80:80
```

---

# Network Commands

List networks:

```bash
docker network ls
```

Inspect:

```bash
docker network inspect bridge
```

Create:

```bash
docker network create app-network
```

Connect:

```bash
docker network connect app-network container
```

Disconnect:

```bash
docker network disconnect app-network container
```

Remove:

```bash
docker network rm app-network
```

Cleanup:

```bash
docker network prune
```

---

# Custom Networks

Benefits:

- Automatic DNS
- Better isolation
- Easier service communication
- Production friendly

---

# Network Security

Best Practices:

- Use custom bridge networks
- Avoid unnecessary port exposure
- Limit host networking
- Segment applications
- Apply least privilege

---

# Production Best Practices

- One network per application stack
- Publish only required ports
- Use overlay networks in clusters
- Separate frontend and backend networks
- Monitor network traffic

---

# Troubleshooting

List networks:

```bash
docker network ls
```

Inspect network:

```bash
docker network inspect app-network
```

Inspect container:

```bash
docker inspect CONTAINER
```

Test connectivity:

```bash
docker exec -it CONTAINER ping web
```

---

# Hands-on Labs

1. Create a custom bridge network.
2. Launch two containers.
3. Verify communication using container names.
4. Publish ports.
5. Inspect the network.
6. Disconnect and reconnect containers.
7. Remove unused networks.

---

# Interview Questions

1. What is Docker networking?
2. Explain the bridge network.
3. Difference between bridge and host network?
4. What is an overlay network?
5. Why use custom networks?
6. How does Docker DNS work?
7. Difference between EXPOSE and -p?
8. What is docker network inspect?
9. How do containers communicate?
10. When should macvlan be used?

---

# Official References

- Docker Networking Documentation
- Docker CLI Reference
- Docker Bridge Network Documentation
- Docker Overlay Network Documentation

---

# Quick Revision

```text
bridge → Default Network

host → Host Stack

none → No Networking

overlay → Multi-host

macvlan → Physical Network Access

docker network ls

docker network inspect

docker network create

docker network connect

docker network prune
```

---

# Status

✅ Docker Networks Guide Completed
