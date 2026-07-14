# 🚀 AWS Storage & Content Delivery Projects

## Real-World Projects for DevOps Engineers

This section contains production-oriented projects built using AWS Storage and Content Delivery services.

The goal is to understand how Amazon S3, Amazon EBS, Amazon EFS, and Amazon CloudFront work together in real cloud environments.

These projects simulate common architectures used by startups and enterprise applications.

---

# Project 01: Static Website Hosting with Amazon S3 & CloudFront

## 📖 Project Overview

Host a highly available static website using Amazon S3 and accelerate global content delivery using Amazon CloudFront.

This architecture removes the need for traditional web servers while providing low latency and high availability.

---

## Problem Statement

Hosting a website on a single server creates several challenges:

- Single point of failure
- Higher latency for global users
- Infrastructure management
- Scaling limitations

CloudFront and Amazon S3 solve these problems by providing serverless website hosting with global content delivery.

---

## Architecture

```text
                    Internet Users

         ┌───────────┼────────────┐

         │           │            │

      India        Europe        USA

         │           │            │

         ▼           ▼            ▼

      Edge Location  Edge Location  Edge Location

                    │

                    ▼

           Amazon CloudFront

                    │

                    ▼

          Amazon S3 Bucket

                    │

         HTML CSS JavaScript Images
```

---

## AWS Services Used

- Amazon S3
- Amazon CloudFront
- AWS Certificate Manager (Optional)
- Amazon Route 53 (Optional)

---

## Implementation Steps

### Step 1

Create an S3 Bucket

Example:

```text
company-static-website
```

---

### Step 2

Upload:

- index.html
- style.css
- images
- JavaScript files

---

### Step 3

Enable Static Website Hosting

Configure:

- Index Document
- Error Document

---

### Step 4

Create CloudFront Distribution

Origin:

```text
Amazon S3 Bucket
```

---

### Step 5

Enable HTTPS

(Optional)

Use AWS Certificate Manager.

---

### Step 6

Test Website

Verify:

- Website loads successfully
- CloudFront URL works
- Cache headers

---

## Skills Learned

✔ Static Website Hosting

✔ CDN

✔ HTTPS

✔ Cache Management

✔ Cloud Architecture

---

# Project 02: Highly Available Shared File System using Amazon EFS

## 📖 Project Overview

Build a highly available web application where multiple EC2 instances share the same application files using Amazon EFS.

This architecture is commonly used for CMS applications, WordPress, Laravel, and container-based workloads.

---

## Problem Statement

When multiple EC2 instances are running behind a Load Balancer:

```text
EC2-1

↓

Upload File

↓

Stored Locally
```

EC2-2 cannot access the uploaded file.

This causes inconsistent application behavior.

Amazon EFS solves this problem.

---

## Architecture

```text
                 Users

                   │

                   ▼

        Application Load Balancer

                   │

        ┌──────────┴──────────┐

        │                     │

     EC2 Instance        EC2 Instance

        │                     │

        └──────────┬──────────┘

                   ▼

              Amazon EFS

                   │

            Shared Application Data
```

---

## AWS Services Used

- Amazon EC2
- Amazon EFS
- Application Load Balancer
- Security Groups

---

## Implementation Steps

### Step 1

Create Amazon EFS

---

### Step 2

Create Mount Targets

One Mount Target for each Availability Zone.

---

### Step 3

Launch EC2 Instances

Install:

```bash
amazon-efs-utils
```

---

### Step 4

Mount Amazon EFS

```bash
sudo mkdir /data

sudo mount -t efs fs-xxxxxxxx:/ /data
```

---

### Step 5

Store Application Files

Example:

```text
WordPress

Uploads

Images

Configuration
```

---

### Step 6

Verify

Create a file from EC2-1.

Confirm the same file is visible from EC2-2.

---

## Skills Learned

✔ Shared Storage

✔ NFS

✔ Multi-Server Applications

✔ High Availability

✔ Linux Mounting

---

# Project 03: Automated Backup & Disaster Recovery using Amazon EBS

## 📖 Project Overview

Protect EC2 data by automatically creating EBS snapshots.

This project demonstrates backup automation and disaster recovery strategies.

---

## Problem Statement

If an EC2 instance fails unexpectedly:

```text
EC2

↓

Disk Failure

↓

Data Loss
```

Regular EBS snapshots minimize downtime and help recover data quickly.

---

## Architecture

```text
EC2 Instance

      │

      ▼

Amazon EBS Volume

      │

      ▼

Snapshot

      │

      ▼

Amazon Data Lifecycle Manager

      │

      ▼

CloudWatch

      │

      ▼

SNS Notification
```

---

## AWS Services Used

- Amazon EC2
- Amazon EBS
- Amazon Data Lifecycle Manager
- Amazon CloudWatch
- Amazon SNS

---

## Implementation Steps

### Step 1

Create an EC2 Instance

---

### Step 2

Attach an Amazon EBS Volume

---

### Step 3

Create Snapshot Policy

Configure:

- Daily Backup
- Weekly Backup
- Retention Period

---

### Step 4

Monitor

CloudWatch monitors snapshot execution.

---

### Step 5

Restore

Create a new EBS Volume from the snapshot.

Attach it to another EC2 instance.

---

## Skills Learned

✔ Backup Strategy

✔ Disaster Recovery

✔ Snapshot Management

✔ Monitoring

✔ Storage Automation

---

# Screenshot Structure

```text
screenshots/

├── project-01-static-website/
│
│   ├── architecture.png
│   ├── s3-bucket.png
│   ├── cloudfront-distribution.png
│   └── website-output.png
│
├── project-02-efs/
│
│   ├── architecture.png
│   ├── efs-created.png
│   ├── mount-target.png
│   └── shared-storage.png
│
└── project-03-backup/
    │
    ├── architecture.png
    ├── ebs-volume.png
    ├── snapshot-created.png
    └── cloudwatch-monitoring.png
```

---

# DevOps Skills Covered

After completing these projects, you will gain practical experience with:

- Amazon S3
- Amazon EBS
- Amazon EFS
- Amazon CloudFront
- Backup Automation
- Disaster Recovery
- CDN
- Shared Storage
- High Availability
- AWS Monitoring
- Production Architecture

---

# Recommended Next Projects

After completing this section, continue with:

### Project 04

Secure Private S3 Bucket using CloudFront + Origin Access Control (OAC)

---

### Project 05

Production 3-Tier Web Application

Services:

- VPC
- EC2
- ALB
- Auto Scaling
- EFS
- RDS
- CloudFront
- IAM
- CloudWatch

---

# Official AWS References

- Amazon S3 User Guide
- Amazon EBS User Guide
- Amazon EFS User Guide
- Amazon CloudFront Developer Guide
- AWS Well-Architected Framework

---

# Status

✅ AWS Storage & Content Delivery Projects Completed

The next section will focus on **AWS Networking & Security**, where you'll build the foundation for production-grade cloud architectures.
