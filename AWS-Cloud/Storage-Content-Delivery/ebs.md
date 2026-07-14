# 💽 Amazon EBS (Elastic Block Store)

# Complete Amazon EBS Guide for DevOps Engineers

Amazon Elastic Block Store (Amazon EBS) is a high-performance block storage service designed specifically for Amazon EC2 instances.

It provides persistent storage that behaves like a physical hard disk attached to a virtual server while offering cloud-native features such as snapshots, encryption, resizing, monitoring, and high availability.

According to AWS, Amazon EBS is designed for workloads that require frequent updates, low latency, and consistent performance.

---

# 📖 What is Amazon EBS?

Imagine purchasing a new computer.

The computer contains:

- CPU
- RAM
- Hard Disk

The hard disk stores:

- Operating System
- Applications
- Files
- Databases

EC2 works the same way.

An EC2 instance needs storage to keep the operating system and application data.

Amazon EBS provides that storage.

```text
Physical Computer

CPU
RAM
Hard Disk

↓

AWS Cloud

EC2
Memory
Amazon EBS
```

Think of Amazon EBS as the **hard drive of an EC2 instance**.

---

# Why Do We Need Amazon EBS?

Without persistent storage:

```text
EC2 Instance

↓

Store Application

↓

Instance Stops

↓

Data Lost
```

This would make running production applications impossible.

Amazon EBS solves this problem by storing data independently from the running instance.

Even if an EC2 instance is stopped or restarted, the data stored on its EBS volume remains available.

---

# Amazon EBS Architecture

```text
                    AWS Region

                        │

            Availability Zone (ap-south-1a)

                        │

                ┌──────────────┐
                │ EC2 Instance │
                └──────┬───────┘
                       │
                 Attached Volume
                       │
                ┌──────────────┐
                │ Amazon EBS   │
                └──────┬───────┘
                       │
                 Snapshot Backup
                       │
                Amazon S3
```

> **Note:** EBS snapshots are internally stored in Amazon S3, but AWS manages this storage for you. You cannot browse snapshot data directly inside an S3 bucket.

---

# Core Components of Amazon EBS

## 1. Volume

A volume is a virtual storage device attached to an EC2 instance.

It stores:

- Operating System
- Applications
- Logs
- Databases
- User Files

Example:

```text
EC2 Instance

↓

Ubuntu Linux

↓

Amazon EBS Volume
```

---

## 2. Snapshot

A snapshot is a point-in-time backup of an EBS volume.

```text
Amazon EBS

↓

Snapshot

↓

Stored Securely

↓

Restore Anytime
```

Snapshots are incremental.

This means:

- First snapshot copies all data.
- Future snapshots only copy changed blocks.

This saves storage space and reduces backup time.

---

## 3. Availability Zone

An EBS volume exists inside one Availability Zone.

Example:

```text
Region

↓

Mumbai

↓

Availability Zone

↓

ap-south-1a

↓

EBS Volume
```

An EBS volume can only be attached to an EC2 instance in the same Availability Zone.

---

# Amazon EBS Volume Types

AWS provides different volume types depending on workload.

---

## General Purpose SSD (gp3)

Recommended for most applications.

Used for:

- Web servers
- Development
- Application servers
- Small databases

Advantages:

- Low latency
- High performance
- Cost-effective

---

## Provisioned IOPS SSD (io2)

Designed for business-critical applications.

Used for:

- Oracle Database
- SQL Server
- SAP
- High transaction workloads

Advantages:

- Extremely high IOPS
- Very low latency
- High durability

---

## Throughput Optimized HDD (st1)

Used for:

- Big data
- Log processing
- Streaming

---

## Cold HDD (sc1)

Used for:

- Archive data
- Infrequently accessed files

Lowest storage cost.

---

# How Amazon EBS Works

When an EC2 instance needs to read or write data:

```text
Application

↓

Operating System

↓

File System

↓

Amazon EBS

↓

AWS Storage Infrastructure
```

AWS automatically replicates EBS data within the same Availability Zone to improve durability.

---

# Attach and Detach Volumes

One EC2 instance can have multiple EBS volumes.

Example:

```text
EC2 Instance

├── Root Volume

├── Data Volume

└── Backup Volume
```

Volumes can also be detached and attached to another EC2 instance within the same Availability Zone.

---

# Root Volume

Every EC2 instance requires a root volume.

The root volume contains:

- Operating System
- Boot Loader
- System Configuration

Example:

```text
Ubuntu EC2

↓

Root Volume (gp3)

↓

Ubuntu Installed
```

---

# Data Volumes

Additional EBS volumes can store:

- Database files
- Application logs
- User uploads
- Backups

Keeping application data separate from the operating system improves management and recovery.

---

# Elastic Volumes

Amazon EBS allows online modifications.

You can:

- Increase storage size
- Change volume type
- Increase IOPS

without stopping the EC2 instance in many cases.

---

# Encryption

Amazon EBS supports encryption using AWS Key Management Service (AWS KMS).

Encrypted data includes:

- Volume data
- Snapshots
- Data transferred between EC2 and EBS

Benefits:

✔ Protects sensitive information  
✔ Meets compliance requirements  
✔ Integrated with AWS KMS  

---

# Snapshots

Snapshots are commonly used for:

- Disaster Recovery
- Backup Automation
- Migration
- Volume Restoration

Example:

```text
EBS Volume

↓

Daily Snapshot

↓

Restore New Volume

↓

Launch New EC2
```

---

# Monitoring Amazon EBS

Amazon CloudWatch monitors:

- Volume Read Operations
- Volume Write Operations
- Read Latency
- Write Latency
- Queue Length
- Burst Balance

Monitoring helps identify storage bottlenecks before they affect applications.

---

# AWS CLI Examples

List volumes:

```bash
aws ec2 describe-volumes
```

Create a volume:

```bash
aws ec2 create-volume \
--size 20 \
--volume-type gp3 \
--availability-zone ap-south-1a
```

Attach volume:

```bash
aws ec2 attach-volume \
--volume-id vol-xxxxxxxx \
--instance-id i-xxxxxxxx \
--device /dev/xvdf
```

Create snapshot:

```bash
aws ec2 create-snapshot \
--volume-id vol-xxxxxxxx
```

---

# DevOps Use Cases

Amazon EBS is commonly used for:

- Linux root filesystem
- Docker host storage
- Jenkins server data
- Kubernetes worker node storage
- Database storage
- Application logs
- CI/CD build servers

---

# Best Practices

✔ Use gp3 for most workloads

✔ Enable encryption

✔ Schedule automatic snapshots

✔ Separate OS and application data

✔ Monitor CloudWatch metrics

✔ Delete unused volumes

✔ Tag volumes properly

✔ Use IAM least privilege

---

# Common Troubleshooting

## Volume Not Attaching

Check:

- Same Availability Zone
- Instance state
- IAM permissions

---

## Disk Not Visible

Linux:

```bash
lsblk
```

Check new disks:

```bash
sudo fdisk -l
```

---

## Filesystem Not Mounted

Mount manually:

```bash
sudo mount /dev/xvdf /data
```

Verify:

```bash
df -h
```

---

# Amazon EBS vs Amazon EFS vs Amazon S3

| Feature | Amazon EBS | Amazon EFS | Amazon S3 |
|----------|------------|------------|-----------|
| Storage Type | Block | File | Object |
| Attached To | EC2 | Multiple EC2 | Any AWS Service |
| Shared Access | No (except Multi-Attach for supported workloads) | Yes | Yes |
| Best For | Operating Systems, Databases | Shared Application Files | Images, Videos, Backups, Static Websites |

---

# Interview Questions

### What is Amazon EBS?

Amazon EBS is a persistent block storage service designed for Amazon EC2 instances.

---

### Is EBS persistent?

Yes.

Data remains even if the EC2 instance is stopped.

---

### Can one EBS volume be attached to multiple EC2 instances?

Normally, no.

Some Provisioned IOPS Multi-Attach volumes support attachment to multiple instances within the same Availability Zone for supported clustered applications.

---

### What is an EBS Snapshot?

A point-in-time backup of an EBS volume stored by AWS.

---

### Which volume type is recommended for most workloads?

General Purpose SSD (gp3).

---

# Screenshot

```text
screenshots/

└── ebs/

    ├── ebs-overview.png

    └── ebs-hands-on-lab.png
```

---

# Official AWS Documentation

- Amazon EBS User Guide
- Amazon EC2 User Guide
- AWS Well-Architected Framework
- AWS CLI Command Reference

---

# Skills Covered

✔ Block Storage

✔ EC2 Storage Management

✔ Snapshots

✔ Encryption

✔ AWS CLI

✔ Backup Strategy

✔ Cloud Monitoring

✔ Production Storage Design

---

# Status

Amazon EBS Completed 💽🚀
