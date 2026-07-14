# 📂 Amazon EFS (Elastic File System)

# Complete Amazon EFS Guide for DevOps Engineers

Amazon Elastic File System (Amazon EFS) is a fully managed, elastic Network File System (NFS) that allows multiple Amazon EC2 instances to access the same shared storage simultaneously.

Unlike Amazon EBS, which is designed for a single EC2 instance, Amazon EFS enables multiple servers to read and write the same files concurrently.

Amazon EFS automatically grows and shrinks as files are added or removed, eliminating the need for storage provisioning.

---

# 📖 What is Amazon EFS?

Imagine a company with multiple application servers.

Each server needs access to:

- Website files
- User uploads
- Configuration files
- Shared application data

If every server stores its own copy:

```text
EC2 1

└── website files

EC2 2

└── website files

EC2 3

└── website files
```

Problems:

❌ Duplicate files

❌ Difficult synchronization

❌ More storage

❌ Manual updates

---

Amazon EFS solves this problem.

```text
                Amazon EFS

                     ▲

         ┌───────────┼───────────┐

         │           │           │

      EC2-1       EC2-2       EC2-3

```

Every server accesses the same shared filesystem.

---

# Why Amazon EFS?

Amazon EFS is designed for workloads that require:

- Shared storage
- High availability
- Automatic scaling
- Multiple server access

Typical applications include:

✔ Web applications

✔ CMS systems

✔ Shared media storage

✔ Container storage

✔ Kubernetes persistent volumes

✔ Machine learning workloads

---

# Amazon EFS Architecture

```text
                    AWS Region

          ┌──────────────────────────┐

          │                          │

 Availability Zone A         Availability Zone B

          │                          │

      Mount Target              Mount Target

          │                          │

      EC2 Instance             EC2 Instance

           \                      /

            \                    /

             ─── Amazon EFS ─────
```

Amazon EFS replicates data across multiple Availability Zones for high availability and durability.

---

# How Amazon EFS Works

Applications write files using the NFS protocol.

```text
Application

↓

Linux File System

↓

NFS Client

↓

Amazon EFS

↓

AWS Storage Infrastructure
```

To Linux, EFS appears as a normal mounted directory.

Example:

```bash
/var/www/html

/data

/shared
```

---

# Core Components

## File System

The main storage resource.

Example:

```text
Project Files

Application Logs

Images

Documents
```

---

## Mount Target

A network endpoint inside a VPC.

Each Availability Zone requires a Mount Target.

```text
AZ-A

↓

Mount Target

↓

Amazon EFS
```

---

## Security Groups

Control network access to EFS.

Required port:

```text
2049 (NFS)
```

Example:

```text
EC2 Security Group

↓

Allow TCP 2049

↓

EFS Security Group
```

---

## Access Points

Access Points simplify application access.

Benefits:

✔ Different users

✔ Different permissions

✔ Separate directories

Example:

```text
Application A

↓

Access Point A

↓

/app1

----------------

Application B

↓

Access Point B

↓

/app2
```

---

# Performance Modes

Amazon EFS offers different performance modes.

## General Purpose

Recommended for:

- Web applications
- CMS
- General workloads

Lowest latency.

---

## Max I/O

Designed for:

- Big data
- Analytics
- Large-scale workloads

Supports higher throughput.

---

# Throughput Modes

## Bursting Throughput

Default mode.

Performance depends on storage size.

---

## Provisioned Throughput

Specify required throughput.

Used when workload is predictable.

---

## Elastic Throughput

Automatically adjusts throughput based on demand.

Ideal for dynamic workloads.

---

# Storage Classes

## Standard

Frequently accessed files.

---

## Infrequent Access (IA)

Lower-cost storage.

Automatically managed using Lifecycle Policies.

---

# Lifecycle Management

Automatically moves files.

```text
30 Days

↓

EFS Standard

↓

EFS IA

↓

Lower Cost
```

---

# Encryption

Supports encryption:

✔ At Rest

✔ In Transit

Uses AWS Key Management Service (AWS KMS).

---

# Monitoring

Amazon CloudWatch provides metrics for:

- Throughput
- Connections
- Storage Size
- Burst Credits
- IOPS

---

# AWS CLI

Create File System:

```bash
aws efs create-file-system
```

Describe File Systems:

```bash
aws efs describe-file-systems
```

Create Mount Target:

```bash
aws efs create-mount-target
```

---

# Mount Amazon EFS on Linux

Install utilities:

Ubuntu

```bash
sudo apt update

sudo apt install amazon-efs-utils
```

Create mount point:

```bash
sudo mkdir /efs
```

Mount:

```bash
sudo mount -t efs fs-xxxxxxxx:/ /efs
```

Verify:

```bash
df -h
```

---

# DevOps Use Cases

Amazon EFS is widely used for:

✔ Kubernetes Persistent Volumes

✔ ECS Shared Storage

✔ Shared Website Files

✔ WordPress Hosting

✔ CI/CD Shared Workspace

✔ Machine Learning Datasets

✔ Media Processing

---

# Best Practices

✔ Create Mount Targets in every AZ

✔ Enable encryption

✔ Use Lifecycle Policies

✔ Monitor CloudWatch metrics

✔ Use Access Points

✔ Restrict Security Groups

✔ Enable backups

---

# Troubleshooting

## Mount Failed

Check:

- Security Group
- Port 2049
- Mount Target
- VPC Configuration

---

## Permission Denied

Check:

- Linux permissions
- Access Point configuration
- Security Group

---

## Slow Performance

Check:

- Performance Mode
- Throughput Mode
- Burst Credits

---

# Amazon EFS vs Amazon EBS

| Feature | Amazon EFS | Amazon EBS |
|----------|------------|------------|
| Storage Type | File | Block |
| Shared Storage | Yes | No (normally) |
| Multiple EC2 | Yes | No |
| Auto Scaling | Yes | Manual resize |
| Protocol | NFS | Block Device |

---

# Interview Questions

### What is Amazon EFS?

A managed Network File System (NFS) that provides shared file storage for multiple EC2 instances.

---

### Which protocol does EFS use?

NFS version 4.x.

---

### Can multiple EC2 instances access the same EFS?

Yes.

This is the primary purpose of Amazon EFS.

---

### Which port does EFS use?

TCP Port 2049.

---

### Difference between EBS and EFS?

EBS is block storage attached to a single EC2 instance.

EFS is shared file storage that multiple EC2 instances can mount simultaneously.

---

# Screenshot

```text
screenshots/

└── efs/

    ├── efs-overview.png

    └── efs-hands-on-lab.png
```

---

# Official AWS References

- Amazon EFS User Guide
- Amazon EC2 User Guide
- AWS Well-Architected Framework

---

# Skills Covered

✔ Shared File Storage

✔ NFS

✔ Mount Targets

✔ Access Points

✔ CloudWatch Monitoring

✔ Linux Mounting

✔ Production Storage Architecture

---

# Status

Amazon EFS Completed 📂🚀
