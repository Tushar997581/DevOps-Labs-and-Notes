# 📦 Docker Registries

> A **Docker Registry** is a service that stores and distributes Docker images. It allows developers and organizations to push, pull, and share container images efficiently.

---

# 📑 Table of Contents

1. Introduction
2. What is a Docker Registry?
3. Why Do We Need a Docker Registry?
4. How Docker Registries Work
5. Registry vs Repository
6. Types of Docker Registries
7. Popular Docker Registries
8. Docker Hub
9. Docker Registry Workflow
10. Common Docker Registry Commands
11. Image Tagging
12. Push & Pull Images
13. Best Practices
14. Common Errors & Troubleshooting
15. Hands-on Lab
16. Interview Questions
17. Quick Revision
18. Official Documentation

---

# 📘 Introduction

A **Docker Registry** is a centralized location where Docker images are stored.

Think of it as **GitHub for Docker Images**.

Instead of storing source code, a Docker Registry stores container images that can be downloaded and used anywhere.

---

# 🤔 What is a Docker Registry?

A Docker Registry is a service that stores Docker images.

It helps developers to:

- Store Docker Images
- Share Images
- Download Images
- Version Images
- Integrate with CI/CD Pipelines

---

# ❓ Why Do We Need a Docker Registry?

Imagine you build a Docker image on your laptop.

Without a registry:

❌ You must manually copy the image to every server.

With a registry:

✅ Build Once

↓

✅ Push to Registry

↓

✅ Pull Anywhere

This makes deployments much faster and easier.

---

# ⚙️ How Docker Registries Work

```text
Dockerfile
      │
docker build
      │
Docker Image
      │
docker push
      │
Docker Registry
      │
docker pull
      │
Docker Container
```

---

# 📂 Registry vs Repository

| Registry | Repository |
|----------|------------|
| Stores multiple repositories | Stores images for one application |
| Example: Docker Hub | Example: nginx |

Example:

```text
Docker Hub
│
├── nginx
├── mysql
├── redis
└── ubuntu
```

Each folder is called a **Repository**.

---

# 🌍 Types of Docker Registries

## 🌐 Public Registry

Anyone can download images.

Examples:

- Docker Hub
- GitHub Container Registry

---

## 🔒 Private Registry

Only authorized users can access images.

Used by companies to store production images securely.

---

# 🚀 Popular Docker Registries

| Registry | Description |
|-----------|-------------|
| Docker Hub | Official Docker Registry |
| Amazon ECR | AWS Container Registry |
| GitHub Container Registry | Registry integrated with GitHub |
| Azure Container Registry | Microsoft Azure Registry |
| Google Artifact Registry | Google Cloud Registry |
| Harbor | Self-hosted Enterprise Registry |

---

# 🐳 Docker Hub

Docker Hub is the official public registry provided by Docker.

### Features

- Public Repositories
- Private Repositories
- Official Docker Images
- Image Versioning
- Team Collaboration

Example:

```bash
docker pull nginx
```

Docker automatically downloads the image from Docker Hub.

---

# 🔄 Docker Registry Workflow

```text
Developer
     │
docker build
     │
Docker Image
     │
docker push
     │
Docker Registry
     │
docker pull
     │
Docker Container
```

---

# 💻 Common Docker Registry Commands

## Login

```bash
docker login
```

---

## Logout

```bash
docker logout
```

---

## Tag an Image

```bash
docker tag myapp:1.0 username/myapp:1.0
```

---

## Push an Image

```bash
docker push username/myapp:1.0
```

---

## Pull an Image

```bash
docker pull username/myapp:1.0
```

---

## Search Images

```bash
docker search nginx
```

---

# 🏷️ Image Tagging

Examples:

```text
myapp:1.0
myapp:1.1
myapp:v2
myapp:latest
```

### ✅ Best Practice

- Use version numbers
- Avoid relying only on `latest`
- Follow Semantic Versioning

---

# 📤 Push & Pull Images

### Push

```bash
docker push username/myapp:v1
```

### Pull

```bash
docker pull username/myapp:v1
```

---

# ✅ Best Practices

- Use meaningful image tags.
- Use private registries for production.
- Keep images updated.
- Scan images for vulnerabilities.
- Remove unused images.
- Don't store secrets inside images.
- Use version numbers instead of `latest`.

---

# 🛠️ Common Errors & Troubleshooting

## Authentication Failed

```bash
docker login
```

Check your Docker Hub username and password.

---

## Access Denied

Verify:

- Repository exists
- Correct username
- Push permissions

---

## Image Not Found

```bash
docker images
```

Check the image name and tag.

---

## Push Rejected

Ensure you tagged the image correctly.

Example:

```bash
docker tag myapp username/myapp:v1
```

---

# 🧪 Hands-on Lab

### Lab 1

- Create a Docker Hub account.
- Login using Docker CLI.

### Lab 2

- Build a Docker image.

### Lab 3

- Tag the image.

### Lab 4

- Push the image to Docker Hub.

### Lab 5

- Delete the local image.

### Lab 6

- Pull the image from Docker Hub.

### Lab 7

- Run the container.

---

# 🎯 Interview Questions

1. What is a Docker Registry?
2. What is Docker Hub?
3. What is the difference between a Registry and a Repository?
4. Why do we use Docker Registries?
5. How do you push an image?
6. How do you pull an image?
7. What is image tagging?
8. What is a private registry?
9. What are the advantages of Docker Hub?
10. Why should you avoid using `latest` in production?

---

# 📝 Quick Revision

```text
Docker Registry → Stores Docker Images

Repository → Collection of Images

Docker Hub → Official Registry

docker login → Login

docker tag → Tag an Image

docker push → Upload Image

docker pull → Download Image

Public Registry → Anyone Can Access

Private Registry → Restricted Access
```

---

# 📚 Official Documentation

- Docker Registry Documentation
- Docker Hub Documentation
- Docker CLI Documentation
- Amazon ECR Documentation
- GitHub Container Registry Documentation

---

## 🎉 Conclusion

Docker Registries make it easy to **store**, **share**, and **deploy** container images. They are an essential part of modern DevOps workflows and CI/CD pipelines. Learning how to use registries effectively helps you build scalable, secure, and production-ready applications.
