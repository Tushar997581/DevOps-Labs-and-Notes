# 🚀 AWS Networking & Security Projects

# Real-World Networking Projects for DevOps Engineers

This section contains hands-on projects that combine Amazon VPC, Subnets, Route Tables, Internet Gateway, NAT Gateway, Security Groups, Network ACLs, Elastic Load Balancing, IAM, AWS WAF, and AWS Shield.

These projects simulate real production environments used by startups and enterprise organizations.

---

# Project 01: Build a Custom VPC

## 📖 Project Overview

Create a secure Amazon VPC from scratch instead of using the default VPC.

This project introduces the basic networking components required for every AWS deployment.

---

## Architecture

```text
                     AWS Region

                         │

                Amazon VPC (10.0.0.0/16)

               ┌─────────┴─────────┐

               │                   │

        Public Subnet       Private Subnet

               │                   │

       Internet Gateway      Route Table
```

---

## AWS Services Used

- Amazon VPC
- Public Subnet
- Private Subnet
- Route Tables
- Internet Gateway

---

## Objectives

- Create a custom VPC
- Configure subnets
- Attach an Internet Gateway
- Configure route tables
- Launch an EC2 instance

---

## Skills Learned

✔ VPC Design

✔ Subnet Planning

✔ Internet Connectivity

✔ Routing

---

# Project 02: Secure Two-Tier Web Application

## 📖 Project Overview

Deploy a web application using public and private subnets.

The web server is publicly accessible, while the application server remains private.

---

## Architecture

```text
                  Internet

                      │

              Internet Gateway

                      │

              Public Subnet

                      │

             EC2 Web Server

                      │

               Security Group

                      │

             Private Subnet

                      │

          EC2 Application Server
```

---

## AWS Services Used

- Amazon VPC
- EC2
- Public Subnet
- Private Subnet
- Security Groups
- Route Tables

---

## Objectives

- Deploy frontend in public subnet
- Deploy backend in private subnet
- Configure Security Groups
- Restrict backend access

---

## Skills Learned

✔ Two-Tier Architecture

✔ Network Isolation

✔ Secure Communication

---

# Project 03: Highly Available Three-Tier Architecture

## 📖 Project Overview

Build a production-ready three-tier application.

---

## Architecture

```text
                      Internet

                          │

                  Internet Gateway

                          │

              Application Load Balancer

                          │

         ┌────────────────┼────────────────┐

         │                │                │

      EC2 (AZ-A)      EC2 (AZ-B)      EC2 (AZ-C)

               │          │          │

                └──── Amazon EFS ────┘

                       │

                  Amazon RDS
```

---

## AWS Services Used

- Amazon VPC
- ALB
- EC2
- Auto Scaling
- Amazon EFS
- Amazon RDS
- Security Groups

---

## Objectives

- Deploy ALB
- Configure Target Groups
- Launch EC2 instances in multiple AZs
- Share files using EFS
- Store application data in RDS

---

## Skills Learned

✔ High Availability

✔ Multi-AZ Deployment

✔ Shared Storage

✔ Load Balancing

---

# Project 04: Private Infrastructure Using NAT Gateway

## 📖 Project Overview

Allow private EC2 instances to access the Internet without exposing them publicly.

---

## Architecture

```text
                   Internet

                       │

                Internet Gateway

                       │

                Public Subnet

                       │

                 NAT Gateway

                       │

             Private Route Table

                       │

             Private EC2 Instance
```

---

## AWS Services Used

- NAT Gateway
- Route Tables
- Public Subnet
- Private Subnet
- EC2

---

## Objectives

- Deploy NAT Gateway
- Configure private routing
- Install software from Internet
- Prevent inbound access

---

## Skills Learned

✔ Private Networking

✔ Secure Internet Access

✔ Route Table Configuration

---

# Project 05: Secure Public Web Application

## 📖 Project Overview

Protect a public web application using AWS WAF and AWS Shield.

---

## Architecture

```text
                   Internet

                       │

                   Route 53

                       │

                  CloudFront

                       │

                 AWS Shield

                       │

                  AWS WAF

                       │

            Application Load Balancer

                       │

                 EC2 Instances
```

---

## AWS Services Used

- CloudFront
- AWS WAF
- AWS Shield
- ALB
- EC2

---

## Objectives

- Configure Web ACL
- Enable Managed Rules
- Enable DDoS Protection
- Monitor blocked requests

---

## Skills Learned

✔ Web Security

✔ DDoS Protection

✔ Layer 7 Security

✔ Production Security

---

# Project 06: IAM-Based Secure Infrastructure

## 📖 Project Overview

Implement secure access management using IAM Users, Groups, Roles, and Policies.

---

## Architecture

```text
               Developers

                    │

               IAM Group

                    │

              IAM Policies

                    │

             EC2 IAM Role

                    │

               Amazon S3
```

---

## AWS Services Used

- IAM
- EC2
- Amazon S3

---

## Objectives

- Create IAM Users
- Create IAM Groups
- Create IAM Roles
- Attach policies
- Access S3 using IAM Role

---

## Skills Learned

✔ IAM Security

✔ Least Privilege

✔ IAM Roles

✔ Temporary Credentials

---

# Complete Production Architecture

```text
                        Internet

                            │

                       Amazon Route 53

                            │

                       CloudFront CDN

                            │

                    AWS Shield + AWS WAF

                            │

                Application Load Balancer

                            │

               Auto Scaling Group (EC2)

          ┌─────────────────┼─────────────────┐

          │                 │                 │

      EC2 (AZ-A)       EC2 (AZ-B)       EC2 (AZ-C)

                │             │             │

                 └────── Amazon EFS ───────┘

                            │

                     Amazon RDS (Private)

                            │

                      Private Subnets

                            │

                      NAT Gateway

                            │

                    Internet Gateway

                            │

                        Amazon VPC
```

---

# Project Summary

| Project | Services Used |
|----------|---------------|
| Custom VPC | VPC, IGW, Route Tables |
| Two-Tier Web App | VPC, EC2, Security Groups |
| Three-Tier Architecture | ALB, EC2, EFS, RDS |
| NAT Gateway Lab | NAT Gateway, Route Tables |
| Secure Web Application | WAF, Shield, CloudFront |
| IAM Infrastructure | IAM, EC2, S3 |

---

# Recommended Screenshot Structure

```text
screenshots/

├── project-01-custom-vpc/
│   ├── architecture.png
│   ├── vpc-created.png
│   ├── subnets.png
│   └── route-table.png
│
├── project-02-two-tier/
│   ├── architecture.png
│   ├── public-server.png
│   ├── private-server.png
│   └── security-groups.png
│
├── project-03-three-tier/
│   ├── architecture.png
│   ├── alb.png
│   ├── target-group.png
│   ├── efs.png
│   └── rds.png
│
├── project-04-nat-gateway/
│   ├── architecture.png
│   ├── nat-gateway.png
│   ├── private-route-table.png
│   └── internet-access.png
│
├── project-05-secure-web/
│   ├── architecture.png
│   ├── waf.png
│   ├── shield.png
│   └── blocked-requests.png
│
└── project-06-iam/
    ├── architecture.png
    ├── iam-user.png
    ├── iam-role.png
    └── s3-access.png
```

---

# DevOps Skills Covered

After completing these projects, you will have practical experience with:

- Amazon VPC
- Public & Private Subnets
- Route Tables
- Internet Gateway
- NAT Gateway
- Security Groups
- Network ACLs
- Elastic Load Balancer
- IAM
- AWS WAF
- AWS Shield
- High Availability
- Multi-AZ Architecture
- Production Security
- AWS Networking

---

# Status

✅ AWS Networking & Security Projects Completed

These projects prepare you for production deployments, DevOps interviews, and AWS certification scenarios.
