# 🌍 Amazon Internet Gateway (IGW)

# Complete AWS Internet Gateway Guide for DevOps Engineers

An Amazon Internet Gateway (IGW) is a highly available, fully managed AWS networking component that enables communication between resources inside an Amazon VPC and the public Internet.

An Internet Gateway allows inbound and outbound IPv4 and IPv6 traffic between your VPC and the Internet.

Without an Internet Gateway, resources inside a VPC cannot communicate directly with the Internet.

---

# 📖 What is an Internet Gateway?

Imagine your company has its own private office.

Employees can communicate with each other inside the office, but they cannot communicate with the outside world unless there is a main entrance.

```text
Office

↓

Main Gate

↓

Public Road

↓

World
```

AWS works similarly.

```text
Amazon VPC

↓

Internet Gateway

↓

Internet
```

The Internet Gateway acts as the main entrance and exit for your VPC.

---

# Why Do We Need an Internet Gateway?

Without an Internet Gateway:

```text
Internet

❌

Cannot reach EC2

EC2

❌

Cannot access Internet
```

Examples:

- Cannot SSH from your laptop
- Cannot open a hosted website
- Cannot download software updates
- Cannot access public APIs

With an Internet Gateway:

```text
Internet

↓

Internet Gateway

↓

Public Subnet

↓

EC2 Instance
```

Communication becomes possible.

---

# Internet Gateway Architecture

```text
                    Internet

                        │

                        ▼

              Internet Gateway

                        │

          Amazon VPC (10.0.0.0/16)

        ┌───────────────┴───────────────┐

        │                               │

 Public Subnet                    Private Subnet

        │                               │

     EC2 Web Server                EC2 App Server
```

Only resources in properly configured **public subnets** can communicate directly with the Internet.

---

# How Internet Gateway Works

When an EC2 instance sends traffic:

```text
EC2

↓

Route Table

↓

Internet Gateway

↓

Internet
```

When a user accesses a public website:

```text
User

↓

Internet

↓

Internet Gateway

↓

Route Table

↓

EC2
```

The Internet Gateway allows this two-way communication.

---

# Components Required for Internet Access

Creating an Internet Gateway alone is **not enough**.

For an EC2 instance to access the Internet, all of the following are required:

### 1. Amazon VPC

The Internet Gateway must be attached to a VPC.

---

### 2. Public Subnet

The EC2 instance must be in a public subnet.

---

### 3. Route Table

The subnet's Route Table must contain:

```text
Destination

0.0.0.0/0

↓

Target

Internet Gateway
```

---

### 4. Public IPv4 Address

The EC2 instance needs:

- Public IPv4 Address

or

- Elastic IP Address

Without a public IP, the Internet cannot return traffic to the instance.

---

### 5. Security Group

Allow required inbound traffic.

Examples:

```text
SSH

22

HTTP

80

HTTPS

443
```

---

# Internet Gateway Attachment

Every Internet Gateway must be attached to a VPC.

```text
Internet Gateway

↓

Attach

↓

Amazon VPC
```

One Internet Gateway can be attached to only one VPC at a time.

---

# Route Table Configuration

Public Route Table:

| Destination | Target |
|-------------|--------|
|10.0.0.0/16|Local|
|0.0.0.0/0|Internet Gateway|

This route allows all Internet-bound traffic to leave through the Internet Gateway.

---

# Public vs Private Subnet

## Public Subnet

```text
EC2

↓

Route Table

↓

Internet Gateway

↓

Internet
```

Internet communication:

✔ Allowed

---

## Private Subnet

```text
EC2

↓

Route Table

↓

NAT Gateway

↓

Internet Gateway

↓

Internet
```

Inbound Internet traffic:

❌ Not allowed

---

# Elastic IP

Elastic IP provides a static public IPv4 address.

Useful for:

- Bastion Hosts
- Public Web Servers
- Fixed DNS records

```text
Elastic IP

↓

EC2

↓

Internet Gateway
```

---

# IPv6 Support

Internet Gateway supports:

- IPv4
- IPv6

For IPv6 Internet access, Route Tables typically use:

```text
::/0
```

as the destination.

---

# AWS CLI

Create Internet Gateway:

```bash
aws ec2 create-internet-gateway
```

Attach Internet Gateway:

```bash
aws ec2 attach-internet-gateway \
--internet-gateway-id igw-xxxxxxxx \
--vpc-id vpc-xxxxxxxx
```

Describe Internet Gateways:

```bash
aws ec2 describe-internet-gateways
```

Detach Internet Gateway:

```bash
aws ec2 detach-internet-gateway \
--internet-gateway-id igw-xxxxxxxx \
--vpc-id vpc-xxxxxxxx
```

Delete Internet Gateway:

```bash
aws ec2 delete-internet-gateway \
--internet-gateway-id igw-xxxxxxxx
```

---

# AWS Console Navigation

```text
AWS Console

↓

VPC

↓

Internet Gateways

↓

Create Internet Gateway

↓

Attach to VPC
```

---

# DevOps Use Cases

Internet Gateway is commonly used for:

✔ Hosting web applications

✔ Public APIs

✔ Bastion Hosts

✔ Jenkins servers

✔ Public Load Balancers

✔ Software updates

✔ Public Docker registries

---

# Best Practices

✔ Attach only one Internet Gateway per VPC

✔ Use public subnets only for Internet-facing resources

✔ Place databases in private subnets

✔ Use Security Groups to restrict access

✔ Use NAT Gateway for private workloads

✔ Enable VPC Flow Logs for troubleshooting

✔ Tag networking resources

---

# Troubleshooting

## Cannot SSH into EC2

Check:

- Internet Gateway attached
- Public IP assigned
- Route Table has `0.0.0.0/0 → IGW`
- Security Group allows TCP 22

---

## Website Not Accessible

Verify:

- EC2 is in a public subnet
- HTTP (80) or HTTPS (443) allowed
- Web server is running
- Route Table is correct

---

## No Internet Access

Check:

- Internet Gateway attachment
- Public Route Table
- Public IPv4 address
- Network ACL
- Security Group

---

# Internet Gateway vs NAT Gateway

| Feature | Internet Gateway | NAT Gateway |
|----------|------------------|-------------|
| Direct Internet Access | Yes | No |
| Inbound Internet Traffic | Yes | No |
| Outbound Internet Traffic | Yes | Yes |
| Used By | Public Subnets | Private Subnets |

---

# Interview Questions

### What is an Internet Gateway?

An Internet Gateway is a managed AWS networking component that enables communication between a VPC and the public Internet.

---

### Can an EC2 instance access the Internet with only an Internet Gateway?

No.

The instance also needs:

- Public subnet
- Route Table
- Public IP
- Security Group

---

### Can one Internet Gateway be attached to multiple VPCs?

No.

One Internet Gateway can only be attached to one VPC at a time.

---

### Does a private subnet use an Internet Gateway directly?

No.

A private subnet typically uses a NAT Gateway for outbound Internet access.

---

# Screenshot

```text
screenshots/

└── internet-gateway/

    ├── igw-overview.png

    └── igw-complete-lab.png
```

---

# Official AWS References

- Amazon VPC User Guide
- AWS Networking Best Practices
- AWS Well-Architected Framework
- AWS CLI Command Reference

---

# Quick Revision

```text
Internet Gateway → Connects VPC to Internet

Attached To → One VPC

Used By → Public Subnets

Route → 0.0.0.0/0 → Internet Gateway

Requires → Public IP + Route Table + Security Group
```

---

# Skills Covered

✔ Internet Gateway

✔ Public Networking

✔ Internet Routing

✔ AWS CLI

✔ Route Tables

✔ Public EC2 Connectivity

✔ Production Networking

---

# Status

Amazon Internet Gateway Completed 🌍🚀
