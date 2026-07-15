# 🌐 AWS Networking & Security

# Complete AWS Networking & Security Guide for DevOps Engineers

Networking is the backbone of every cloud infrastructure.

No matter whether you are deploying a web application, Kubernetes cluster, database, CI/CD pipeline, or microservices, everything depends on a properly designed network.

AWS provides a secure and highly available networking platform that allows organizations to build isolated cloud environments, connect resources securely, control traffic flow, and protect applications from cyber threats.

This section covers AWS Networking and Security from a DevOps Engineer's perspective using AWS best practices and production-ready architectures.

---

# 📖 Why Networking is Important?

Imagine building a company office.

You need:

- Roads
- Buildings
- Security Gates
- Employees
- Visitors
- CCTV
- Firewalls

AWS networking works in a similar way.

Instead of physical infrastructure, AWS provides virtual networking components.

```text
Company Office

Roads
Buildings
Security Gate

↓

AWS Cloud

VPC
Subnets
Security Groups
Route Tables
Internet Gateway
```

Without networking:

❌ EC2 cannot communicate

❌ Applications cannot reach users

❌ Databases become inaccessible

❌ Internet access is impossible

---

# AWS Networking Architecture

```text
                     Internet

                         │

                  Internet Gateway

                         │

               Amazon VPC (10.0.0.0/16)

        ┌────────────────┴────────────────┐

        │                                 │

 Public Subnet                     Private Subnet

        │                                 │

 Application Load Balancer          EC2 Application

                                          │

                                     Amazon RDS

                                          │

                                    NAT Gateway
```

---

# What is Amazon VPC?

Amazon Virtual Private Cloud (Amazon VPC) allows you to create an isolated virtual network inside AWS.

Think of a VPC as your own private data center inside the AWS Cloud.

Inside a VPC, you control:

- IP Address Range
- Subnets
- Route Tables
- Internet Access
- Security
- DNS
- Network Traffic

Learn:

➡️ [Amazon VPC](./vpc.md)

---

# Public & Private Subnets

A subnet divides a VPC into smaller networks.

### Public Subnet

Resources can communicate directly with the Internet.

Examples:

- Bastion Host
- Load Balancer
- NAT Gateway

### Private Subnet

Resources cannot receive direct Internet traffic.

Examples:

- EC2 Application Servers
- Databases
- Internal Services

Learn:

➡️ [Subnets](./subnets.md)

---

# Route Tables

Route Tables decide where network traffic should go.

Example:

```text
Destination

↓

Route Table

↓

Target
```

Possible targets:

- Internet Gateway
- NAT Gateway
- Local Route
- VPC Peering

Learn:

➡️ [Route Tables](./route-tables.md)

---

# Internet Gateway (IGW)

Internet Gateway enables communication between your VPC and the Internet.

Without an Internet Gateway:

```text
EC2

↓

No Internet Access
```

With an Internet Gateway:

```text
EC2

↓

Internet Gateway

↓

Internet
```

Learn:

➡️ [Internet Gateway](./internet-gateway.md)

---

# NAT Gateway

NAT Gateway allows resources inside private subnets to access the Internet without exposing them to incoming Internet traffic.

Typical uses:

- Software updates
- Package installation
- Downloading dependencies

Learn:

➡️ [NAT Gateway](./nat-gateway.md)

---

# Security Groups

Security Groups act as virtual firewalls for AWS resources.

They control:

- Inbound Traffic
- Outbound Traffic

Example:

```text
Internet

↓

Security Group

↓

EC2
```

Common Rules:

- SSH (22)
- HTTP (80)
- HTTPS (443)

Learn:

➡️ [Security Groups](./security-groups.md)

---

# Network ACLs

Network ACLs provide subnet-level security.

Unlike Security Groups:

- Stateless
- Allow Rules
- Deny Rules

Used for additional network protection.

Learn:

➡️ [Network ACLs](./network-acls.md)

---

# Elastic Load Balancing

Elastic Load Balancing distributes incoming traffic across multiple targets.

Types:

- Application Load Balancer (ALB)
- Network Load Balancer (NLB)
- Gateway Load Balancer (GWLB)

Benefits:

✔ High Availability

✔ Fault Tolerance

✔ Automatic Traffic Distribution

Learn:

➡️ [Elastic Load Balancer](./elastic-load-balancer.md)

---

# AWS IAM

Identity and Access Management controls who can access AWS resources.

IAM provides:

- Users
- Groups
- Roles
- Policies
- MFA

Learn:

➡️ [AWS IAM](./iam.md)

---

# AWS WAF

AWS Web Application Firewall protects applications from common web attacks.

Examples:

- SQL Injection
- Cross-Site Scripting (XSS)
- IP Blocking
- Rate Limiting

Learn:

➡️ [AWS WAF](./waf.md)

---

# AWS Shield

AWS Shield protects applications against Distributed Denial of Service (DDoS) attacks.

Available Editions:

- Shield Standard
- Shield Advanced

Learn:

➡️ [AWS Shield](./shield.md)

---

# Service Comparison

| Service | Purpose |
|----------|---------|
| Amazon VPC | Private Network |
| Subnets | Network Segmentation |
| Route Tables | Traffic Routing |
| Internet Gateway | Internet Access |
| NAT Gateway | Outbound Internet |
| Security Groups | Instance Firewall |
| Network ACL | Subnet Firewall |
| ELB | Load Balancing |
| IAM | Identity & Access |
| WAF | Web Protection |
| Shield | DDoS Protection |

---

# Complete Production Architecture

```text
                     Internet
                         │
                  Internet Gateway
                         │
          ┌──────────────┴──────────────┐
          │                             │
     Public Subnet A               Public Subnet B
          │                             │
          └────── Application Load Balancer ──────┐
                                                  │
                ┌─────────────────────────────────┴────────────────────────────────┐
                │                                                                  │
         Private Subnet A                                                   Private Subnet B
                │                                                                  │
           EC2 Application                                                   EC2 Application
                │                                                                  │
                └──────────────────── Amazon EFS ──────────────────────────────────┘
                                   Shared File Storage
                                           │
                                     Amazon RDS
```

---

# AWS CLI Examples

Create VPC

```bash
aws ec2 create-vpc \
--cidr-block 10.0.0.0/16
```

Describe Subnets

```bash
aws ec2 describe-subnets
```

Describe Security Groups

```bash
aws ec2 describe-security-groups
```

Describe Load Balancers

```bash
aws elbv2 describe-load-balancers
```

---

# Security Best Practices

✔ Use least privilege IAM policies

✔ Never expose databases publicly

✔ Use private subnets for application servers

✔ Restrict SSH access

✔ Enable Multi-Factor Authentication (MFA)

✔ Enable VPC Flow Logs

✔ Enable AWS CloudTrail

✔ Use AWS WAF for public applications

✔ Enable AWS Shield

---

# Real DevOps Use Cases

AWS Networking is used for:

- Three-Tier Architecture
- Kubernetes Clusters (Amazon EKS)
- CI/CD Infrastructure
- Hybrid Cloud Connectivity
- VPN Connections
- Secure Production Deployments
- Microservices Architecture

---

# Interview Revision

### What is Amazon VPC?

A logically isolated virtual network in AWS where you launch AWS resources securely.

---

### Difference between Public and Private Subnet?

Public Subnet:

Has a route to an Internet Gateway.

Private Subnet:

Does not have a direct route to an Internet Gateway.

---

### Difference between Security Group and Network ACL?

Security Group:

- Stateful
- Instance Level

Network ACL:

- Stateless
- Subnet Level

---

### What is NAT Gateway?

A managed service that allows resources in private subnets to access the Internet while preventing unsolicited inbound connections.

---

# Screenshot Structure

```text
screenshots/

├── vpc/
├── subnets/
├── route-tables/
├── internet-gateway/
├── nat-gateway/
├── security-groups/
├── network-acls/
├── elastic-load-balancer/
├── iam/
├── waf/
└── shield/
```

---

# Projects Included

- Build a Custom VPC
- Highly Available 3-Tier Architecture
- Private EC2 with NAT Gateway
- Secure Load Balancer Architecture
- IAM Best Practices Lab

---

# Official AWS References

- Amazon VPC User Guide
- Elastic Load Balancing User Guide
- AWS IAM User Guide
- AWS WAF Developer Guide
- AWS Shield Documentation
- AWS Well-Architected Framework

---

# Skills Covered

✔ Amazon VPC

✔ Subnet Design

✔ Internet Connectivity

✔ Routing

✔ Load Balancing

✔ IAM

✔ AWS Security

✔ Production Architecture

---

# Status

🌐 AWS Networking & Security Learning Started 🚀
