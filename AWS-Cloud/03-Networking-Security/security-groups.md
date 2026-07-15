# 🛡️ Amazon Security Groups

# Complete AWS Security Groups Guide for DevOps Engineers

Amazon Security Groups act as virtual firewalls that control inbound and outbound network traffic for AWS resources such as EC2 instances, RDS databases, Application Load Balancers, and Amazon EFS.

A Security Group allows only the traffic that you explicitly define. By default, all inbound traffic is denied, while all outbound traffic is allowed.

Security Groups are **stateful**, meaning if an incoming request is allowed, the response is automatically allowed without requiring an additional outbound rule.

---

# 📖 What is a Security Group?

Imagine an office building.

Every visitor must pass through a security gate.

The security guard checks:

- Who is entering?
- Which door can they use?
- Which room can they access?

AWS Security Groups work similarly.

```text
Internet

↓

Security Group

↓

EC2 Instance
```

Only approved traffic is allowed to reach the instance.

---

# Why Do We Need Security Groups?

Without a firewall:

```text
Internet

↓

EC2

↓

Everything Allowed
```

Problems:

❌ Unauthorized access

❌ Brute-force attacks

❌ Data theft

❌ Increased security risk

With Security Groups:

```text
Internet

↓

Security Group

↓

Allowed Traffic Only

↓

EC2
```

Benefits:

✔ Improved security

✔ Controlled access

✔ Least privilege networking

✔ Easy management

---

# Security Group Architecture

```text
                     Internet

                         │

                Security Group

         ┌──────────┼──────────┐

         │          │          │

     SSH (22)   HTTP (80)  HTTPS (443)

         │          │          │

         ▼          ▼          ▼

               EC2 Instance
```

---

# How Security Groups Work

Whenever traffic reaches an AWS resource:

```text
Incoming Packet

↓

Security Group

↓

Rule Match

↓

Allow or Deny
```

Only matching **allow** rules are permitted.

---

# Stateful Firewall

Security Groups are **stateful**.

Example:

```text
Laptop

↓

SSH Request

↓

EC2
```

Return traffic is automatically allowed.

You do **not** need to create another outbound rule for the response.

---

# Security Group Rules

Every rule contains:

- Protocol
- Port
- Source or Destination

Example:

| Type | Protocol | Port | Source |
|------|----------|------|--------|
| SSH | TCP | 22 | Your IP |
| HTTP | TCP | 80 | 0.0.0.0/0 |
| HTTPS | TCP | 443 | 0.0.0.0/0 |

---

# Inbound Rules

Inbound rules control traffic entering a resource.

Example:

```text
Internet

↓

Port 22

↓

EC2
```

Typical ports:

| Service | Port |
|----------|------|
| SSH | 22 |
| HTTP | 80 |
| HTTPS | 443 |
| MySQL | 3306 |
| PostgreSQL | 5432 |
| RDP | 3389 |

---

# Outbound Rules

Outbound rules control traffic leaving a resource.

Examples:

- Package downloads
- API calls
- Software updates
- Database connections

Default:

```text
All Traffic

↓

Allowed
```

Many organizations restrict outbound traffic for security.

---

# Security Group Association

A Security Group can be attached to:

- EC2 Instances
- RDS Databases
- Load Balancers
- Lambda (inside VPC)
- Amazon EFS

One Security Group can protect multiple resources.

An EC2 instance can also have multiple Security Groups attached.

---

# Security Group Referencing

Instead of allowing IP addresses, Security Groups can reference other Security Groups.

Example:

```text
ALB Security Group

↓

EC2 Security Group

↓

Allow HTTP
```

Benefits:

✔ Better security

✔ Easier management

✔ Dynamic updates

---

# Example Architecture

```text
Internet

↓

Application Load Balancer

↓

ALB Security Group

↓

EC2 Security Group

↓

Application Server

↓

Database Security Group

↓

Amazon RDS
```

Each layer allows only the required traffic.

---

# AWS CLI

Create Security Group:

```bash
aws ec2 create-security-group \
--group-name web-sg \
--description "Web Security Group" \
--vpc-id vpc-xxxxxxxx
```

Authorize SSH:

```bash
aws ec2 authorize-security-group-ingress \
--group-id sg-xxxxxxxx \
--protocol tcp \
--port 22 \
--cidr YOUR_PUBLIC_IP/32
```

Describe Security Groups:

```bash
aws ec2 describe-security-groups
```

Delete Security Group:

```bash
aws ec2 delete-security-group \
--group-id sg-xxxxxxxx
```

---

# AWS Console Navigation

```text
AWS Console

↓

EC2

↓

Security Groups

↓

Create Security Group
```

---

# DevOps Use Cases

Security Groups are used for:

✔ EC2 access

✔ Load Balancer protection

✔ RDS access control

✔ Kubernetes worker nodes

✔ Jenkins servers

✔ Bastion Hosts

✔ Amazon EFS

---

# Best Practices

✔ Allow only required ports

✔ Restrict SSH to your public IP

✔ Use Security Group references instead of broad CIDR ranges

✔ Never expose databases to the Internet

✔ Remove unused rules

✔ Review Security Groups regularly

✔ Use descriptive names and tags

✔ Follow the principle of least privilege

---

# Troubleshooting

## Cannot SSH into EC2

Check:

- TCP Port 22 allowed
- Correct source IP
- EC2 has a public IP
- Network ACL
- Route Table

---

## Website Not Loading

Verify:

- Port 80 or 443 allowed
- Web server running
- Internet Gateway
- Route Table

---

## Database Connection Failed

Check:

- Database Security Group
- Application Security Group
- Correct port (3306, 5432, etc.)

---

# Security Groups vs Network ACLs

| Feature | Security Group | Network ACL |
|----------|----------------|-------------|
| Level | Instance | Subnet |
| Stateful | Yes | No |
| Allow Rules | Yes | Yes |
| Deny Rules | No | Yes |
| Evaluation | All rules | Rule number order |

---

# Interview Questions

### What is a Security Group?

A Security Group is a stateful virtual firewall that controls inbound and outbound traffic for AWS resources.

---

### Are Security Groups stateful?

Yes.

Return traffic is automatically allowed.

---

### Can an EC2 instance have multiple Security Groups?

Yes.

Multiple Security Groups can be attached to the same EC2 instance.

---

### Can Security Groups deny traffic?

No.

Security Groups support only **allow** rules.

To explicitly deny traffic, use a Network ACL or AWS WAF depending on the use case.

---

### Which service protects EC2 at the instance level?

Security Groups.

---

# Screenshot

```text
screenshots/

└── security-groups/

    ├── security-group-overview.png

    └── security-group-complete-lab.png
```

---

# Official AWS References

- Amazon EC2 User Guide
- Amazon VPC User Guide
- AWS Security Best Practices
- AWS Well-Architected Framework
- AWS CLI Command Reference

---

# Quick Revision

```text
Security Group → Instance Firewall

State → Stateful

Supports → Allow Rules Only

Attached To → EC2, RDS, ALB, EFS

Common Ports:

22 → SSH

80 → HTTP

443 → HTTPS

3306 → MySQL
```

---

# Skills Covered

✔ Security Groups

✔ Inbound Rules

✔ Outbound Rules

✔ Stateful Firewall

✔ Least Privilege

✔ EC2 Security

✔ AWS Networking

---

# Status

Amazon Security Groups Completed 🛡️🚀
