# 🌐 Amazon VPC Subnets

# Complete AWS Subnets Guide for DevOps Engineers

A subnet is a logical subdivision of an Amazon Virtual Private Cloud (VPC).

Subnets help organize AWS resources, improve security, isolate workloads, and build highly available architectures.

Every Amazon EC2 instance, RDS database, Load Balancer, and NAT Gateway is launched inside a subnet.

---

# 📖 What is a Subnet?

Think of a VPC as a large city.

Inside the city, there are different areas for different purposes.

Example:

```text
City

├── Residential Area

├── Commercial Area

├── Industrial Area

└── Government Area
```

AWS works similarly.

```text
Amazon VPC

├── Public Subnet

├── Private Subnet

└── Database Subnet
```

Each subnet has its own role.

---

# Why Do We Need Subnets?

Imagine putting everything into one network.

```text
Internet

↓

One Network

↓

Web Server

↓

Application Server

↓

Database
```

Problems:

❌ Poor security

❌ Difficult management

❌ No isolation

❌ Increased attack surface

Subnets solve these problems by separating resources into different networks.

---

# AWS Subnet Architecture

```text
                Amazon VPC

              10.0.0.0/16

       ┌──────────┴──────────┐

       │                     │

 Public Subnet A      Private Subnet A

 10.0.1.0/24          10.0.2.0/24

       │                     │

 Internet Gateway      NAT Gateway

       │                     │

 Load Balancer         EC2 Application

                              │

                           Amazon RDS
```

---

# How Subnets Work

Every subnet receives a portion of the VPC CIDR block.

Example:

VPC:

```text
10.0.0.0/16
```

Possible subnets:

```text
Public

10.0.1.0/24

Private

10.0.2.0/24

Database

10.0.3.0/24
```

Each subnet has its own IP address range.

---

# Public Subnet

A Public Subnet has a route to an Internet Gateway.

```text
Internet

↓

Internet Gateway

↓

Public Subnet

↓

EC2
```

Resources inside a Public Subnet can:

✔ Access the Internet

✔ Receive traffic from the Internet

Typical resources:

- Bastion Host
- Application Load Balancer
- NAT Gateway
- Public EC2

---

# Private Subnet

A Private Subnet has **no direct route** to an Internet Gateway.

```text
Internet

↓

Internet Gateway

↓

Public Subnet

↓

NAT Gateway

↓

Private Subnet

↓

EC2
```

Resources:

✔ Can access the Internet through NAT Gateway

✔ Cannot receive incoming Internet traffic directly

Typical resources:

- Application Servers
- Databases
- Internal APIs
- Kubernetes Worker Nodes

---

# Database Subnet

A Database Subnet is a special private subnet used only for databases.

```text
Application Server

↓

Amazon RDS
```

Benefits:

✔ Better security

✔ Isolation

✔ Compliance

---

# Availability Zones

Subnets exist inside Availability Zones.

Example:

```text
Mumbai Region

↓

Availability Zone A

↓

Public Subnet A

↓

Private Subnet A

----------------------

Availability Zone B

↓

Public Subnet B

↓

Private Subnet B
```

Using multiple Availability Zones increases fault tolerance.

---

# Subnet CIDR

Each subnet has its own CIDR block.

Example:

```text
VPC

10.0.0.0/16

↓

Public

10.0.1.0/24

↓

Private

10.0.2.0/24

↓

Database

10.0.3.0/24
```

The subnet CIDR must be within the VPC CIDR range and must not overlap with another subnet.

---

# Reserved IP Addresses

AWS reserves five IP addresses in every subnet.

Example:

Subnet:

```text
10.0.1.0/24
```

Reserved:

```text
10.0.1.0

10.0.1.1

10.0.1.2

10.0.1.3

10.0.1.255
```

These addresses cannot be assigned to your resources.

---

# Public IP Assignment

When launching an EC2 instance, you can enable automatic public IP assignment.

```text
EC2

↓

Public Subnet

↓

Public IP

↓

Internet Access
```

Without a public IP, an EC2 instance cannot be reached directly from the Internet.

---

# Route Table Association

Every subnet must be associated with a Route Table.

```text
Subnet

↓

Route Table

↓

Destination

↓

Target
```

The Route Table determines how traffic leaves the subnet.

---

# Security

Subnets work together with:

- Security Groups
- Network ACLs

```text
Internet

↓

Security Group

↓

Subnet

↓

EC2
```

Security Groups protect resources, while Network ACLs protect the subnet itself.

---

# AWS CLI

Create a subnet:

```bash
aws ec2 create-subnet \
--vpc-id vpc-xxxxxxxx \
--cidr-block 10.0.1.0/24 \
--availability-zone ap-south-1a
```

Describe subnets:

```bash
aws ec2 describe-subnets
```

Delete a subnet:

```bash
aws ec2 delete-subnet \
--subnet-id subnet-xxxxxxxx
```

---

# Real DevOps Use Cases

Subnets are used to:

✔ Separate frontend and backend services

✔ Protect databases

✔ Build three-tier applications

✔ Deploy Kubernetes clusters

✔ Improve security

✔ Increase availability

---

# Best Practices

✔ Use separate public and private subnets

✔ Place databases in private subnets

✔ Use multiple Availability Zones

✔ Avoid overlapping CIDR blocks

✔ Tag subnets clearly

✔ Restrict Internet-facing resources

✔ Keep sensitive workloads private

---

# Troubleshooting

## EC2 Cannot Access Internet

Check:

- Route Table
- Internet Gateway
- NAT Gateway
- Public IP
- Security Group

---

## Cannot Launch Resource

Verify:

- Available IP addresses
- Correct Availability Zone
- Valid subnet CIDR

---

## CIDR Conflict

Ensure the subnet CIDR does not overlap with existing subnets.

---

# Public vs Private Subnet

| Feature | Public Subnet | Private Subnet |
|----------|---------------|----------------|
| Internet Access | Yes | Through NAT Gateway |
| Public IP | Yes | No |
| Typical Resources | ALB, Bastion Host | EC2, RDS |
| Security | Internet-facing | Internal only |

---

# Interview Questions

### What is a subnet?

A subnet is a logical subdivision of a VPC used to organize and isolate AWS resources.

---

### What is the difference between a Public and Private Subnet?

A Public Subnet has a route to an Internet Gateway.

A Private Subnet does not have a direct route to an Internet Gateway.

---

### Can two subnets have the same CIDR block?

No.

Subnet CIDR blocks within the same VPC must not overlap.

---

### Why are multiple Availability Zones recommended?

To improve high availability and fault tolerance.

---

### How many IP addresses does AWS reserve in every subnet?

AWS reserves five IP addresses in each subnet.

---

# Screenshot

```text
screenshots/

└── subnets/

    ├── subnet-overview.png

    └── subnet-complete-lab.png
```

---

# Official AWS References

- Amazon VPC User Guide
- AWS Well-Architected Framework
- AWS Networking Best Practices
- AWS CLI Command Reference

---

# Skills Covered

✔ Subnet Design

✔ CIDR Planning

✔ Public & Private Networks

✔ High Availability

✔ Multi-AZ Architecture

✔ AWS Networking Fundamentals

---

# Status

Amazon VPC Subnets Completed 🌐🚀
