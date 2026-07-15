# 🌐 Amazon VPC (Virtual Private Cloud)

# Complete Amazon VPC Guide for DevOps Engineers

Amazon Virtual Private Cloud (Amazon VPC) is a service that allows you to create your own isolated virtual network inside AWS.

A VPC gives you complete control over your network, including IP address ranges, subnets, routing, Internet access, and security.

Every production application running on AWS starts with a well-designed VPC.

---

# 📖 What is Amazon VPC?

Imagine you are building a new company office.

You need:

- Land
- Buildings
- Roads
- Security Gates
- Parking
- Electricity

Now imagine building the same office in AWS.

AWS provides the infrastructure, but you design the network.

```text
Physical Office

Land
Roads
Buildings
Security

↓

AWS Cloud

VPC
Subnets
Route Tables
Security Groups
```

Think of a VPC as your **private network inside AWS**.

---

# Why Do We Need a VPC?

Without a VPC:

```text
Application

↓

Public Internet

↓

No Isolation

↓

Security Risk
```

With a VPC:

```text
Internet

↓

VPC

↓

Secure Resources

↓

Controlled Access
```

Benefits:

✔ Network Isolation

✔ Secure Communication

✔ Custom IP Addressing

✔ Fine-Grained Traffic Control

✔ High Availability

---

# Amazon VPC Architecture

```text
                    AWS Region

                         │

                 Amazon VPC

                10.0.0.0/16

         ┌──────────┴──────────┐

         │                     │

 Public Subnet           Private Subnet

         │                     │

    Load Balancer          EC2 Server

                                  │

                            Amazon RDS
```

---

# Components of Amazon VPC

A VPC is built using several networking components.

```text
Amazon VPC

│

├── CIDR Block

├── Subnets

├── Route Tables

├── Internet Gateway

├── NAT Gateway

├── Security Groups

├── Network ACL

├── Elastic IP

└── VPC Endpoints
```

Each component has a specific role in controlling network communication.

---

# CIDR Block

Every VPC must have an IP address range.

Example:

```text
10.0.0.0/16
```

This range is called the CIDR block.

CIDR determines how many private IP addresses are available in your VPC.

Examples:

```text
10.0.0.0/16

172.31.0.0/16

192.168.0.0/16
```

Choose a CIDR block carefully to avoid overlap with other networks.

---

# Default VPC vs Custom VPC

## Default VPC

Created automatically by AWS.

Features:

- One public subnet in each Availability Zone
- Internet Gateway attached
- Ready for quick testing

---

## Custom VPC

Created by the user.

Advantages:

✔ Better security

✔ Full network control

✔ Production-ready design

---

# Public and Private Subnets

A VPC is divided into subnets.

### Public Subnet

Resources have Internet access.

Examples:

- Bastion Host
- Load Balancer
- NAT Gateway

---

### Private Subnet

Resources do not receive direct Internet traffic.

Examples:

- EC2 Application Servers
- Amazon RDS
- Internal Services

---

# Internet Gateway

An Internet Gateway connects a VPC to the Internet.

```text
Internet

↓

Internet Gateway

↓

Public Subnet
```

Without an Internet Gateway, Internet communication is not possible.

---

# Route Tables

Route Tables decide where network traffic goes.

Example:

```text
Destination

↓

Route Table

↓

Target
```

Targets can be:

- Internet Gateway
- NAT Gateway
- Local Route
- VPC Peering

---

# Security Groups

Security Groups protect AWS resources.

Example:

```text
Internet

↓

Security Group

↓

EC2
```

They control:

- Inbound Traffic
- Outbound Traffic

---

# Network ACLs

Network ACLs provide subnet-level security.

Unlike Security Groups:

- Stateless
- Allow Rules
- Deny Rules

---

# Availability Zones

A VPC spans an entire AWS Region.

Subnets exist inside Availability Zones.

Example:

```text
Mumbai Region

↓

AZ-a

AZ-b

AZ-c
```

Using multiple Availability Zones improves availability and fault tolerance.

---

# DNS in VPC

Amazon VPC supports:

- DNS Resolution
- DNS Hostnames

This allows EC2 instances to communicate using DNS names instead of IP addresses.

---

# VPC Peering

VPC Peering connects two VPCs privately.

```text
VPC A

↓

VPC Peering

↓

VPC B
```

Traffic does not pass through the Internet.

---

# VPC Endpoints

VPC Endpoints allow private access to AWS services.

Example:

```text
Private EC2

↓

VPC Endpoint

↓

Amazon S3
```

Benefits:

✔ No Internet Gateway required

✔ Secure communication

---

# AWS CLI

Create a VPC:

```bash
aws ec2 create-vpc \
--cidr-block 10.0.0.0/16
```

Describe VPCs:

```bash
aws ec2 describe-vpcs
```

Delete a VPC:

```bash
aws ec2 delete-vpc \
--vpc-id vpc-xxxxxxxx
```

---

# DevOps Use Cases

Amazon VPC is used for:

✔ Production Applications

✔ Kubernetes (Amazon EKS)

✔ CI/CD Pipelines

✔ Secure Databases

✔ Hybrid Cloud

✔ Microservices

✔ Multi-Tier Architectures

---

# Best Practices

✔ Use Custom VPCs for production

✔ Plan CIDR blocks carefully

✔ Use multiple Availability Zones

✔ Keep databases in private subnets

✔ Restrict SSH access

✔ Enable VPC Flow Logs

✔ Tag networking resources

✔ Follow least privilege principles

---

# Troubleshooting

## EC2 Cannot Access Internet

Check:

- Internet Gateway
- Route Table
- Public IP
- Security Group

---

## Resources Cannot Communicate

Verify:

- Route Tables
- Security Groups
- Network ACLs

---

## Overlapping CIDR Blocks

Choose a different CIDR range before creating the VPC.

---

# Interview Questions

### What is Amazon VPC?

A logically isolated virtual network in AWS where you launch AWS resources securely.

---

### What is CIDR?

CIDR (Classless Inter-Domain Routing) defines the IP address range of a network.

---

### Difference between Default VPC and Custom VPC?

Default VPC:

Automatically created by AWS.

Custom VPC:

Created and managed by the user for production environments.

---

### Can one VPC span multiple Availability Zones?

Yes.

A VPC spans an entire AWS Region, while subnets are created inside individual Availability Zones.

---

# Screenshot

```text
screenshots/

└── vpc/

    ├── vpc-overview.png

    └── vpc-complete-lab.png
```

---

# Official AWS References

- Amazon VPC User Guide
- AWS Well-Architected Framework
- AWS Networking Best Practices
- AWS CLI Command Reference

---

# Skills Covered

✔ Amazon VPC

✔ CIDR Planning

✔ Network Isolation

✔ Public & Private Networking

✔ Internet Connectivity

✔ AWS Networking Architecture

---

# Status

Amazon VPC Completed 🌐🚀
