# 🐳 Docker Hub

> Docker Hub is the official cloud-based container registry provided by Docker. It allows developers to store, manage, share, and distribute Docker images.

---

# 📑 Table of Contents

1. Introduction
2. What is Docker Hub?
3. Why Docker Hub?
4. Docker Hub Features
5. Docker Hub Architecture
6. Docker Hub Account
7. Public vs Private Repositories
8. Official Images
9. Repository Management
10. Docker Hub Workflow
11. Common Docker Hub Commands
12. Best Practices
13. Common Errors & Troubleshooting
14. Hands-on Lab
15. Interview Questions
16. Quick Revision
17. Official Documentation

---

# 📘 Introduction

Docker Hub is the **official container registry** developed by Docker.

It is the default registry used by Docker to store and distribute container images.

Millions of developers use Docker Hub to share images and deploy applications.

---

# 🤔 What is Docker Hub?

Docker Hub is a cloud-based repository where Docker images are stored.

It allows you to:

- Store Docker Images
- Share Images
- Download Images
- Version Images
- Collaborate with Teams
- Integrate with CI/CD Pipelines

---

# ❓ Why Docker Hub?

Without Docker Hub:

❌ Images must be copied manually.

With Docker Hub:

✅ Build Image

↓

✅ Push to Docker Hub

↓

✅ Pull from Anywhere

This makes deployments faster and easier.

---

# ⭐ Docker Hub Features

- Public Repositories
- Private Repositories
- Official Images
- Verified Publisher Images
- Teams & Organizations
- Image Versioning
- Automated Builds
- Webhooks
- Vulnerability Scanning

---

# 🏗 Docker Hub Architecture

```text
Developer
     │
docker build
     │
Docker Image
     │
docker push
     │
Docker Hub
     │
docker pull
     │
Container
```

---

# 👤 Docker Hub Account

To use Docker Hub:

1. Create an account
2. Verify your email
3. Login using Docker CLI

```bash
docker login
```

Logout

```bash
docker logout
```

---

# 📂 Public vs Private Repository

| Public Repository | Private Repository |
|-------------------|--------------------|
| Anyone can pull images | Restricted access |
| Free | Limited in free plans |
| Good for Open Source | Good for Production |

---

# ✅ Official Images

Official Images are maintained by Docker and trusted partners.

Examples:

- nginx
- ubuntu
- mysql
- redis
- postgres
- alpine
- node
- python

Pull Example:

```bash
docker pull nginx
```

---

# 📁 Repository Management

Create Repository

- Choose Public or Private
- Add Description
- Push Images
- Manage Tags

Example:

```text
username/
└── my-app
    ├── latest
    ├── v1.0
    └── v2.0
```

---

# 🔄 Docker Hub Workflow

```text
Write Dockerfile

↓

docker build

↓

Docker Image

↓

docker tag

↓

docker push

↓

Docker Hub

↓

docker pull

↓

Run Container
```

---

# 💻 Common Commands

Login

```bash
docker login
```

Search

```bash
docker search nginx
```

Pull

```bash
docker pull nginx
```

Tag

```bash
docker tag myapp username/myapp:v1
```

Push

```bash
docker push username/myapp:v1
```

Logout

```bash
docker logout
```

---

# ✅ Best Practices

- Use Official Images
- Keep Images Updated
- Use Version Tags
- Avoid Using latest in Production
- Scan Images Regularly
- Remove Unused Images
- Enable Two-Factor Authentication

---

# 🛠 Common Errors

### Login Failed

```bash
docker login
```

Verify your username and password.

---

### Access Denied

Check repository permissions.

---

### Push Failed

Verify image tag.

```bash
docker images
```

---

### Rate Limit Exceeded

- Authenticate with Docker Hub
- Upgrade your Docker Hub plan if required

---

# 🧪 Hands-on Lab

### Lab 1

Create a Docker Hub account.

### Lab 2

Login using Docker CLI.

### Lab 3

Create a repository.

### Lab 4

Build an image.

### Lab 5

Tag the image.

### Lab 6

Push the image.

### Lab 7

Delete the local image.

### Lab 8

Pull the image again.

### Lab 9

Run the container.

---

# 🎯 Interview Questions

1. What is Docker Hub?
2. What are Official Images?
3. Difference between Public and Private Repository?
4. How do you push an image to Docker Hub?
5. What is image tagging?
6. Why avoid `latest` in production?
7. What are Verified Publisher images?
8. How do you authenticate with Docker Hub?
9. What is the default Docker Registry?
10. How do you manage image versions?

---

# 📝 Quick Revision

```text
Docker Hub → Official Docker Registry

docker login

docker search

docker pull

docker tag

docker push

docker logout

Public Repository

Private Repository

Official Images
```

---

# 📚 Official Documentation

- Docker Hub Documentation
- Docker CLI Documentation
- Docker Hub Pricing
- Docker Hub Official Images

---

## 🎉 Conclusion

Docker Hub is the most widely used container registry for storing and sharing Docker images. It simplifies application deployment, enables collaboration, and integrates seamlessly with modern DevOps and CI/CD workflows.
