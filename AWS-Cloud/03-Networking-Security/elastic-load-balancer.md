# ⚖️ Elastic Load Balancing (ELB)

# Complete AWS Elastic Load Balancing Guide for DevOps Engineers

Elastic Load Balancing (ELB) is a fully managed AWS service that automatically distributes incoming application traffic across multiple targets such as Amazon EC2 instances, containers, IP addresses, and AWS Lambda functions.

By distributing traffic across multiple resources, ELB improves application availability, fault tolerance, scalability, and performance.

Elastic Load Balancing continuously monitors the health of registered targets and routes traffic only to healthy resources.

---

# 📖 What is Load Balancing?

Imagine a restaurant with only one cashier.

```text
Customers

↓

Cashier

↓

Long Waiting Time
```

As the number of customers increases, the cashier becomes overloaded.

Now imagine three cashiers.

```text
Customers

↓

Reception Manager

↓

Cashier 1

Cashier 2

Cashier 3
```

Customers are distributed evenly.

AWS uses the same concept.

```text
Users

↓

Load Balancer

↓

EC2-1

EC2-2

EC2-3
```

Instead of one server handling all traffic, the Load Balancer distributes requests across multiple servers.

---

# Why Do We Need a Load Balancer?

Without ELB:

```text
Users

↓

Single EC2

↓

Server Failure

↓

Application Down
```

Problems:

❌ Single Point of Failure

❌ Poor Scalability

❌ High Server Load

❌ Downtime

With ELB:

```text
Users

↓

Elastic Load Balancer

↓

EC2-1

EC2-2

EC2-3
```

Benefits:

✔ High Availability

✔ Fault Tolerance

✔ Automatic Traffic Distribution

✔ Horizontal Scaling

---

# Elastic Load Balancing Architecture

```text
                    Internet

                        │

                        ▼

            Application Load Balancer

                        │

          ┌─────────────┼─────────────┐

          │             │             │

      EC2-1         EC2-2         EC2-3

          │             │             │

         Healthy      Healthy      Healthy
```

---

# Types of Elastic Load Balancers

AWS provides three types of Load Balancers.

```text
Elastic Load Balancing

│

├── Application Load Balancer (ALB)

├── Network Load Balancer (NLB)

└── Gateway Load Balancer (GWLB)
```

---

# 1. Application Load Balancer (ALB)

Application Load Balancer works at **Layer 7 (Application Layer)** of the OSI Model.

It understands:

- HTTP
- HTTPS
- URLs
- Hostnames
- HTTP Headers

Architecture:

```text
Users

↓

ALB

↓

/api

↓

EC2 API Server

----------------

/images

↓

EC2 Image Server
```

Features:

✔ Path-based routing

✔ Host-based routing

✔ HTTPS termination

✔ WebSockets

✔ HTTP/2 support

Used for:

- Web Applications
- REST APIs
- Microservices
- Containers (Amazon ECS, Amazon EKS)

---

# 2. Network Load Balancer (NLB)

Network Load Balancer works at **Layer 4 (Transport Layer)**.

Supports:

- TCP
- UDP
- TLS

Architecture:

```text
Clients

↓

Network Load Balancer

↓

Database Servers
```

Features:

✔ Very low latency

✔ Millions of requests

✔ Static IP support

✔ High performance

Used for:

- Gaming Servers
- Financial Applications
- IoT
- Real-time Systems

---

# 3. Gateway Load Balancer (GWLB)

Gateway Load Balancer works with virtual network appliances.

Examples:

- Firewalls
- Intrusion Detection Systems
- Deep Packet Inspection

Architecture:

```text
Traffic

↓

Gateway Load Balancer

↓

Firewall Appliance

↓

Application
```

Used for:

- Network Security
- Traffic Inspection
- Third-party Security Appliances

---

# Components of an ELB

## Listener

A Listener checks for incoming connections on a specific protocol and port.

Example:

```text
HTTPS

Port 443
```

Example:

```text
HTTP

Port 80
```

---

## Target Group

A Target Group contains the resources that receive traffic.

Targets can be:

- EC2 Instances
- IP Addresses
- AWS Lambda Functions

Architecture:

```text
Target Group

↓

EC2-1

EC2-2

EC2-3
```

---

## Health Checks

ELB continuously checks whether targets are healthy.

Example:

```text
Health Check

↓

/health

↓

200 OK

↓

Healthy
```

If an instance becomes unhealthy:

```text
ELB

↓

Stop Sending Traffic

↓

Healthy EC2 Only
```

---

# Request Flow

```text
User

↓

DNS

↓

Load Balancer

↓

Listener

↓

Target Group

↓

Healthy EC2 Instance
```

---

# SSL/TLS Termination

Application Load Balancer supports HTTPS.

Certificates are managed using:

- AWS Certificate Manager (ACM)

Architecture:

```text
User

↓

HTTPS

↓

ALB

↓

HTTP

↓

EC2
```

Benefits:

✔ Encryption

✔ Simpler certificate management

✔ Improved security

---

# Cross-Zone Load Balancing

Cross-Zone Load Balancing distributes traffic evenly across targets in multiple Availability Zones.

```text
AZ-A

↓

EC2

------------

AZ-B

↓

EC2

------------

ALB

↓

Equal Distribution
```

Improves utilization and resilience.

---

# Sticky Sessions

Sticky Sessions allow a user to continue communicating with the same backend instance for a period of time.

Useful for:

- Shopping carts
- User sessions
- Legacy applications

---

# AWS CLI

Create Target Group:

```bash
aws elbv2 create-target-group \
--name web-target-group \
--protocol HTTP \
--port 80 \
--vpc-id vpc-xxxxxxxx
```

Describe Load Balancers:

```bash
aws elbv2 describe-load-balancers
```

Describe Target Groups:

```bash
aws elbv2 describe-target-groups
```

Register EC2 Target:

```bash
aws elbv2 register-targets \
--target-group-arn TARGET_GROUP_ARN \
--targets Id=i-xxxxxxxx
```

---

# AWS Console Navigation

```text
AWS Console

↓

EC2

↓

Load Balancers

↓

Create Load Balancer

↓

Choose:

Application

Network

Gateway
```

---

# DevOps Use Cases

Elastic Load Balancing is used for:

✔ High Availability

✔ Auto Scaling

✔ Kubernetes Ingress

✔ ECS Services

✔ Multi-AZ Deployments

✔ Blue-Green Deployments

✔ Zero-Downtime Deployments

✔ Microservices

---

# Best Practices

✔ Deploy across multiple Availability Zones

✔ Enable Health Checks

✔ Use HTTPS with ACM

✔ Enable Access Logs

✔ Configure Security Groups

✔ Use Target Groups

✔ Enable Cross-Zone Load Balancing

✔ Monitor CloudWatch Metrics

---

# Monitoring

Amazon CloudWatch provides metrics:

- Request Count
- Healthy Host Count
- UnHealthy Host Count
- Target Response Time
- HTTP 4XX Errors
- HTTP 5XX Errors
- Active Connections

---

# Troubleshooting

## Target Unhealthy

Check:

- Health Check Path
- Security Group
- Web Server Status
- Target Group Port

---

## Website Not Accessible

Verify:

- DNS
- Listener
- Target Group
- Security Group
- Route Table

---

## SSL Certificate Error

Check:

- ACM Certificate
- Listener Configuration
- Domain Validation

---

# ALB vs NLB vs GWLB

| Feature | ALB | NLB | GWLB |
|----------|-----|------|-------|
| OSI Layer | Layer 7 | Layer 4 | Layer 3/4 (Gateway integration) |
| Protocols | HTTP, HTTPS | TCP, UDP, TLS | IP traffic to virtual appliances |
| Routing | Path & Host | Port & Protocol | Network Appliances |
| Target Types | EC2, IP, Lambda | EC2, IP | Virtual Appliances |
| Best For | Web Apps | High Performance | Security Appliances |

---

# Interview Questions

### What is Elastic Load Balancing?

Elastic Load Balancing is an AWS service that automatically distributes incoming traffic across multiple targets to improve availability and scalability.

---

### What are the types of Load Balancers?

- Application Load Balancer (ALB)
- Network Load Balancer (NLB)
- Gateway Load Balancer (GWLB)

---

### Which Load Balancer supports path-based routing?

Application Load Balancer (ALB).

---

### What is a Target Group?

A logical group of backend resources (EC2, IP addresses, or Lambda functions) that receive traffic from the Load Balancer.

---

### What happens if an EC2 instance becomes unhealthy?

The Load Balancer stops routing traffic to that instance until it becomes healthy again.

---

# Screenshot

```text
screenshots/

└── elastic-load-balancer/

    ├── alb-overview.png
    ├── nlb-overview.png
    ├── gwlb-overview.png
    └── elastic-load-balancer-complete-lab.png
```

---

# Official AWS References

- Elastic Load Balancing User Guide
- Application Load Balancer Guide
- Network Load Balancer Guide
- Gateway Load Balancer Guide
- AWS Well-Architected Framework
- AWS CLI Command Reference

---

# Quick Revision

```text
ALB → Layer 7 → HTTP/HTTPS

NLB → Layer 4 → TCP/UDP

GWLB → Security Appliances

Listener → Receives Requests

Target Group → Backend Resources

Health Check → Monitors Target Status
```

---

# Skills Covered

✔ Elastic Load Balancing

✔ Application Load Balancer

✔ Network Load Balancer

✔ Gateway Load Balancer

✔ Health Checks

✔ Target Groups

✔ HTTPS Termination

✔ High Availability

✔ Production Networking

---

# Status

Elastic Load Balancing Completed ⚖️🚀
