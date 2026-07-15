# 🚧 Amazon Network ACLs (Network Access Control Lists)

# Complete AWS Network ACL Guide for DevOps Engineers

Amazon Network Access Control Lists (Network ACLs or NACLs) are optional security layers that control inbound and outbound network traffic at the **subnet level** within an Amazon Virtual Private Cloud (Amazon VPC).

Unlike Security Groups, which protect individual resources, Network ACLs protect an entire subnet.

Network ACLs are **stateless**, meaning return traffic must be explicitly allowed by separate rules.

---

# 📖 What is a Network ACL?

Imagine a company office.

Before anyone enters the building, there is a security checkpoint at the main gate.

Everyone entering or leaving the building is inspected.

```text
Internet

↓

Security Gate

↓

Office Building

↓

Employees
```

AWS works similarly.

```text
Internet

↓

Network ACL

↓

Subnet

↓

EC2 Instance
```

The Network ACL filters traffic before it reaches resources inside the subnet.

---

# Why Do We Need Network ACLs?

Suppose multiple EC2 instances exist inside a subnet.

Instead of configuring security separately for every instance, AWS allows you to apply subnet-wide filtering.

Benefits:

✔ Additional security layer

✔ Subnet-level protection

✔ Allow rules

✔ Deny rules

✔ Centralized network filtering

---

# Network ACL Architecture

```text
                    Internet

                        │

                Internet Gateway

                        │

                 Public Route Table

                        │

                 Network ACL

                        │

                 Public Subnet

                        │

                  Security Group

                        │

                    EC2 Instance
```

Traffic passes through the Network ACL before reaching the Security Group.

---

# How Network ACL Works

Incoming traffic:

```text
Internet

↓

Network ACL

↓

Security Group

↓

EC2
```

Outgoing traffic:

```text
EC2

↓

Security Group

↓

Network ACL

↓

Internet
```

---

# Stateless Firewall

Network ACLs are **stateless**.

Example:

```text
Laptop

↓

SSH Request

↓

EC2
```

Inbound Rule:

```text
Allow TCP 22
```

Outbound Rule:

Must also allow the return traffic.

Unlike Security Groups, return traffic is **not** automatically allowed.

---

# Components of a Network ACL

A Network ACL contains:

- Rule Number
- Protocol
- Port Range
- Source/Destination
- Allow or Deny

Example:

| Rule | Protocol | Port | Source | Action |
|------|----------|------|--------|--------|
|100|TCP|22|Your IP|ALLOW|
|110|TCP|80|0.0.0.0/0|ALLOW|
|120|All|All|0.0.0.0/0|DENY|

---

# Rule Evaluation

Rules are processed in ascending numerical order.

Example:

```text
Rule 100

↓

Rule 110

↓

Rule 120
```

The first matching rule is applied.

---

# Inbound Rules

Inbound rules control traffic entering the subnet.

Typical examples:

| Service | Port |
|----------|------|
|SSH|22|
|HTTP|80|
|HTTPS|443|
|MySQL|3306|

---

# Outbound Rules

Outbound rules control traffic leaving the subnet.

Examples:

- Software updates
- API requests
- Package downloads
- Database communication

Because Network ACLs are stateless, outbound rules must allow response traffic.

---

# Default Network ACL

Every VPC contains a Default Network ACL.

Features:

✔ Allows all inbound traffic

✔ Allows all outbound traffic

You can modify the rules if needed.

---

# Custom Network ACL

Production environments typically use custom Network ACLs.

Example:

Public Subnet ACL

```text
Allow HTTP

Allow HTTPS

Allow SSH

Deny All Others
```

Private Subnet ACL

```text
Allow Application Traffic

Allow Database Traffic

Deny Internet Access
```

---

# Association

Each subnet must be associated with one Network ACL.

One Network ACL can protect multiple subnets.

```text
Network ACL

↓

Subnet A

↓

Subnet B

↓

Subnet C
```

---

# AWS CLI

Create Network ACL:

```bash
aws ec2 create-network-acl \
--vpc-id vpc-xxxxxxxx
```

Describe Network ACLs:

```bash
aws ec2 describe-network-acls
```

Create Inbound Rule:

```bash
aws ec2 create-network-acl-entry \
--network-acl-id acl-xxxxxxxx \
--rule-number 100 \
--protocol tcp \
--port-range From=22,To=22 \
--cidr-block YOUR_PUBLIC_IP/32 \
--rule-action allow \
--ingress
```

Delete Network ACL:

```bash
aws ec2 delete-network-acl \
--network-acl-id acl-xxxxxxxx
```

---

# AWS Console Navigation

```text
AWS Console

↓

VPC

↓

Network ACLs

↓

Create Network ACL

↓

Associate Subnet
```

---

# DevOps Use Cases

Network ACLs are commonly used for:

✔ Subnet protection

✔ Blocking malicious IP ranges

✔ Compliance requirements

✔ Multi-tier architectures

✔ Additional security beyond Security Groups

✔ Enterprise network segmentation

---

# Best Practices

✔ Use custom Network ACLs for production

✔ Keep rule numbers organized

✔ Leave gaps (100, 110, 120...) for future rules

✔ Allow only required traffic

✔ Use Deny rules carefully

✔ Test rule changes before production deployment

✔ Document rule purpose

---

# Troubleshooting

## Cannot SSH into EC2

Check:

- Network ACL inbound rule for TCP 22
- Network ACL outbound ephemeral ports
- Security Group
- Route Table
- Internet Gateway

---

## Website Not Accessible

Verify:

- HTTP (80) and HTTPS (443) allowed
- Subnet association
- Security Group configuration

---

## Database Connection Failed

Check:

- Network ACL rules
- Database Security Group
- Correct port
- Route Table

---

# Security Groups vs Network ACLs

| Feature | Security Group | Network ACL |
|----------|----------------|-------------|
| Level | Instance | Subnet |
| Stateful | Yes | No |
| Supports Deny Rules | No | Yes |
| Rule Evaluation | All allow rules | Number order |
| Default Behavior | Deny inbound | Allow inbound & outbound (default ACL) |

---

# Interview Questions

### What is a Network ACL?

A subnet-level firewall that controls inbound and outbound traffic in a VPC.

---

### Are Network ACLs stateful?

No.

Network ACLs are stateless.

Return traffic must be explicitly allowed.

---

### Can a Network ACL deny traffic?

Yes.

Network ACLs support both **Allow** and **Deny** rules.

---

### Can one Network ACL be associated with multiple subnets?

Yes.

A single Network ACL can be associated with multiple subnets.

---

### What is the main difference between Security Groups and Network ACLs?

Security Groups protect resources and are stateful.

Network ACLs protect subnets and are stateless.

---

# Screenshot

```text
screenshots/

└── network-acls/

    ├── network-acl-overview.png

    └── network-acl-complete-lab.png
```

---

# Official AWS References

- Amazon VPC User Guide
- AWS Security Best Practices
- AWS Well-Architected Framework
- AWS CLI Command Reference

---

# Quick Revision

```text
Network ACL → Subnet Firewall

Level → Subnet

State → Stateless

Supports → Allow & Deny Rules

Rule Processing → Lowest Rule Number First

Association → One ACL per Subnet
```

---

# Skills Covered

✔ Network ACLs

✔ Stateless Firewall

✔ Subnet Security

✔ Allow & Deny Rules

✔ Rule Evaluation

✔ AWS Networking Security

---

# Status

Amazon Network ACLs Completed 🚧🚀
