# 🛣️ Amazon VPC Route Tables

# Complete AWS Route Tables Guide for DevOps Engineers

Amazon VPC Route Tables determine how network traffic travels within a Virtual Private Cloud (VPC). Every subnet in a VPC must be associated with a Route Table, which acts as a routing policy for that subnet.

A Route Table contains a set of rules called **routes**. Each route specifies a destination network and the target where the traffic should be sent.

Without Route Tables, resources inside a VPC would not know where to send or receive network traffic.

---

# 📖 What is a Route Table?

Imagine you are driving in a city.

Road signs tell you:

- Which road to take
- Which direction to travel
- Where your destination is

A Route Table works the same way.

```text
Network Packet

        │

        ▼

Route Table

        │

Destination Match

        │

        ▼

Correct Target
```

Every packet leaving an EC2 instance is checked against the Route Table.

---

# Why Do We Need Route Tables?

Without Route Tables:

```text
EC2

↓

Destination Unknown

↓

Packet Dropped
```

With Route Tables:

```text
EC2

↓

Route Table

↓

Internet Gateway

↓

Internet
```

Benefits:

✔ Controls network traffic

✔ Enables Internet access

✔ Connects private resources

✔ Supports hybrid networking

---

# Route Table Architecture

```text
                    Amazon VPC

                  10.0.0.0/16

         ┌────────────┴────────────┐

         │                         │

 Public Subnet              Private Subnet

         │                         │

Public Route Table      Private Route Table

         │                         │

Internet Gateway        NAT Gateway
```

---

# Components of a Route Table

Every route contains:

- Destination
- Target

Example:

| Destination | Target |
|-------------|--------|
|10.0.0.0/16|Local|
|0.0.0.0/0|Internet Gateway|

---

# Local Route

When a VPC is created, AWS automatically adds a Local Route.

Example:

```text
Destination

10.0.0.0/16

↓

Target

Local
```

Purpose:

Allows communication between resources inside the same VPC.

---

# Internet Route

To allow Internet access:

```text
Destination

0.0.0.0/0

↓

Target

Internet Gateway
```

This route is normally used in Public Subnets.

---

# NAT Gateway Route

Private subnets use a NAT Gateway.

```text
Destination

0.0.0.0/0

↓

NAT Gateway
```

Benefits:

✔ Outbound Internet access

✔ No inbound Internet access

---

# Route Table Association

Every subnet must be associated with exactly one Route Table.

```text
Subnet

↓

Route Table

↓

Routes Applied
```

A Route Table can be associated with multiple subnets if they require the same routing behavior.

---

# Main Route Table

Each VPC has one Main Route Table.

If you do not explicitly associate a subnet with another Route Table, AWS automatically associates it with the Main Route Table.

---

# Custom Route Tables

Production environments often use multiple Route Tables.

Example:

```text
Public Route Table

↓

Internet Gateway

-----------------------

Private Route Table

↓

NAT Gateway
```

This separation improves security and management.

---

# Route Priority

AWS evaluates routes using the **most specific match**.

Example:

| Destination | Target |
|-------------|--------|
|10.0.1.0/24|VPC Peering|
|10.0.0.0/16|Local|
|0.0.0.0/0|Internet Gateway|

Traffic to `10.0.1.0/24` uses the first route because it is more specific.

---

# Common Route Targets

A Route Table can send traffic to:

- Local
- Internet Gateway (IGW)
- NAT Gateway
- VPC Peering
- Transit Gateway
- Virtual Private Gateway
- VPC Endpoint

---

# Public Route Table

```text
Destination

10.0.0.0/16

↓

Local

----------------

0.0.0.0/0

↓

Internet Gateway
```

Used by:

- Public EC2
- Bastion Host
- Load Balancer

---

# Private Route Table

```text
Destination

10.0.0.0/16

↓

Local

----------------

0.0.0.0/0

↓

NAT Gateway
```

Used by:

- Application Servers
- Databases
- Internal Services

---

# AWS CLI

Create Route Table:

```bash
aws ec2 create-route-table \
--vpc-id vpc-xxxxxxxx
```

Create Route:

```bash
aws ec2 create-route \
--route-table-id rtb-xxxxxxxx \
--destination-cidr-block 0.0.0.0/0 \
--gateway-id igw-xxxxxxxx
```

Associate Route Table:

```bash
aws ec2 associate-route-table \
--subnet-id subnet-xxxxxxxx \
--route-table-id rtb-xxxxxxxx
```

Describe Route Tables:

```bash
aws ec2 describe-route-tables
```

---

# DevOps Use Cases

Route Tables are used for:

✔ Internet connectivity

✔ Private application networks

✔ Hybrid cloud

✔ Multi-tier applications

✔ Kubernetes networking

✔ VPC Peering

---

# Best Practices

✔ Use separate Route Tables for public and private subnets

✔ Keep databases in private subnets

✔ Review routes regularly

✔ Avoid unnecessary Internet routes

✔ Tag Route Tables clearly

✔ Follow least privilege networking

---

# Troubleshooting

## EC2 Cannot Access Internet

Check:

- Internet Gateway attached
- Route Table has `0.0.0.0/0 → IGW`
- Public IP assigned
- Security Group rules

---

## Private EC2 Cannot Download Updates

Check:

- NAT Gateway exists
- Route Table points to NAT Gateway
- NAT Gateway is in a Public Subnet

---

## Wrong Route

Verify:

- Correct Route Table association
- Correct destination CIDR
- Correct target

---

# Public vs Private Route Table

| Feature | Public Route Table | Private Route Table |
|----------|--------------------|---------------------|
| Internet Route | Internet Gateway | NAT Gateway |
| Used By | Public Subnets | Private Subnets |
| Inbound Internet | Yes | No |
| Outbound Internet | Yes | Yes |

---

# Interview Questions

### What is a Route Table?

A Route Table is a collection of routing rules that determines where network traffic is directed within a VPC.

---

### What is the Local Route?

A route automatically created by AWS that enables communication between resources inside the same VPC.

---

### Can multiple subnets share one Route Table?

Yes.

Multiple subnets can be associated with the same Route Table if they require identical routing behavior.

---

### What is the difference between a Public and Private Route Table?

A Public Route Table routes Internet traffic through an Internet Gateway.

A Private Route Table routes Internet-bound traffic through a NAT Gateway.

---

# Screenshot

```text
screenshots/

└── route-tables/

    ├── route-table-overview.png

    └── route-table-complete-lab.png
```

---

# Official AWS References

- Amazon VPC User Guide
- AWS Networking Best Practices
- AWS CLI Command Reference
- AWS Well-Architected Framework

---

# Skills Covered

✔ Route Tables

✔ Local Routes

✔ Internet Routing

✔ NAT Gateway Routing

✔ Public & Private Networks

✔ AWS Networking

---

# Status

Amazon VPC Route Tables Completed 🛣️🚀
