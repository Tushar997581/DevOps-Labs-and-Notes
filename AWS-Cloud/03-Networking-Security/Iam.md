# 🔐 AWS Identity and Access Management (IAM)

# Complete AWS IAM Guide for DevOps Engineers

AWS Identity and Access Management (IAM) is a global AWS service that enables you to securely control access to AWS resources.

IAM allows you to create users, groups, roles, and policies so that only authorized people and applications can access AWS services.

It follows the **Principle of Least Privilege**, meaning users and applications should receive only the permissions they need to perform their tasks.

---

# 📖 What is IAM?

Imagine a company office.

Not every employee has access to every room.

```text
Company Office

↓

Security Desk

↓

Employee ID Card

↓

Allowed Rooms
```

AWS works the same way.

```text
User

↓

IAM

↓

AWS Resources
```

IAM decides:

- Who can log in
- Which AWS services they can use
- What actions they can perform
- Which resources they can access

---

# Why Do We Need IAM?

Without IAM:

```text
Everyone

↓

Full AWS Access

↓

Security Risk
```

Problems:

❌ Accidental deletion of resources

❌ Unauthorized access

❌ Data leakage

❌ No accountability

With IAM:

```text
User

↓

IAM Policy

↓

Limited Permissions

↓

AWS Resource
```

Benefits:

✔ Secure access

✔ Fine-grained permissions

✔ Multi-user management

✔ Auditability

✔ Least privilege

---

# Authentication vs Authorization

## Authentication

Authentication verifies **who you are**.

Examples:

- Username & Password
- Access Key
- MFA

---

## Authorization

Authorization determines **what you are allowed to do**.

Example:

```text
Developer

↓

Can Launch EC2

Cannot Delete VPC
```

IAM handles both authentication and authorization.

---

# IAM Architecture

```text
                     AWS Account

                           │

                           ▼

                         IAM

        ┌──────────────┼──────────────┐

        │              │              │

      Users         Groups         Roles

        │              │              │

        └──────────────┼──────────────┘

                       ▼

                    Policies

                       ▼

                AWS Resources

      EC2   S3   RDS   Lambda   CloudWatch
```

---

# IAM Components

## Root User

The root user is created automatically when an AWS account is created.

Characteristics:

- Full access to all AWS services
- Cannot be restricted by IAM policies
- Should not be used for daily work

Best Practices:

✔ Enable MFA

✔ Do not create access keys

✔ Use only for account-level tasks

---

## IAM Users

An IAM User represents a person or application.

Example:

```text
John

↓

IAM User

↓

Amazon EC2 Access
```

Users have:

- Username
- Password (optional)
- Access Keys (optional)
- Permissions

---

## IAM Groups

Groups simplify permission management.

Instead of assigning permissions individually:

```text
Developers

↓

Developer Group

↓

EC2 Access
```

Example Groups:

- Developers
- DevOps
- Administrators
- ReadOnly

---

## IAM Roles

IAM Roles provide temporary credentials.

Roles are commonly used by:

- EC2
- Lambda
- ECS
- EKS
- Cross-account access

Example:

```text
EC2

↓

IAM Role

↓

Amazon S3
```

No access keys are stored on the instance.

---

# IAM Policies

Policies define permissions.

A policy contains:

- Effect
- Action
- Resource

Example:

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": [
        "s3:ListBucket"
      ],
      "Resource": "*"
    }
  ]
}
```

---

# Types of Policies

### AWS Managed Policies

Created and maintained by AWS.

Example:

- AmazonS3ReadOnlyAccess
- AmazonEC2FullAccess

---

### Customer Managed Policies

Created by your organization.

Reusable across multiple users and roles.

---

### Inline Policies

Attached directly to a single user, group, or role.

Generally used for special cases.

---

# IAM Policy Evaluation

AWS evaluates requests in this order:

1. Authentication
2. Policy Evaluation
3. Explicit Deny
4. Allow
5. Default Deny

Example:

```text
User

↓

IAM Policy

↓

Allow EC2

↓

EC2 Launch
```

---

# IAM Roles Deep Dive

Roles are preferred over access keys.

Example:

```text
EC2 Instance

↓

IAM Role

↓

Temporary Credentials

↓

Amazon S3
```

Benefits:

✔ More secure

✔ Automatically rotated credentials

✔ No hardcoded secrets

---

# Multi-Factor Authentication (MFA)

MFA adds an extra security layer.

Authentication requires:

```text
Password

+

OTP

↓

Login
```

Supported methods:

- Authenticator App
- Hardware Token
- FIDO Security Key

---

# Password Policy

A strong password policy should require:

- Minimum length
- Uppercase letters
- Lowercase letters
- Numbers
- Special characters
- Password rotation (if required by your organization)

---

# Access Keys

Access Keys are used by:

- AWS CLI
- SDKs
- Applications

Structure:

```text
Access Key ID

Secret Access Key
```

Best Practices:

✔ Rotate regularly

✔ Never commit to GitHub

✔ Prefer IAM Roles when possible

---

# AWS CLI Authentication

Configure CLI:

```bash
aws configure
```

Example:

```text
AWS Access Key ID

AWS Secret Access Key

Region

Output Format
```

Verify:

```bash
aws sts get-caller-identity
```

---

# Monitoring with CloudTrail

AWS CloudTrail records IAM activity.

Examples:

- Login events
- Policy changes
- User creation
- Role assumption

Useful for:

- Auditing
- Security investigations
- Compliance

---

# AWS CLI

Create User:

```bash
aws iam create-user \
--user-name devops-user
```

Create Group:

```bash
aws iam create-group \
--group-name developers
```

Attach Policy:

```bash
aws iam attach-group-policy \
--group-name developers \
--policy-arn arn:aws:iam::aws:policy/AmazonEC2ReadOnlyAccess
```

List Users:

```bash
aws iam list-users
```

---

# AWS Console Navigation

```text
AWS Console

↓

IAM

↓

Users

↓

Groups

↓

Roles

↓

Policies
```

---

# DevOps Use Cases

IAM is used for:

✔ Secure AWS access

✔ EC2 IAM Roles

✔ CI/CD Pipelines

✔ GitHub Actions

✔ Terraform Authentication

✔ Cross-Account Access

✔ Lambda Permissions

✔ Kubernetes (EKS) IAM Roles

---

# Best Practices

✔ Never use the Root User for daily work

✔ Enable MFA

✔ Follow Least Privilege

✔ Use IAM Roles instead of Access Keys

✔ Rotate credentials

✔ Remove unused users

✔ Enable CloudTrail

✔ Review permissions regularly

---

# Troubleshooting

## Access Denied

Check:

- IAM Policy
- Resource ARN
- Explicit Deny
- SCP (AWS Organizations, if applicable)

---

## AWS CLI Authentication Failed

Verify:

- Access Keys
- Region
- IAM permissions
- AWS CLI configuration

---

## EC2 Cannot Access S3

Check:

- IAM Role attached
- Trust Policy
- S3 permissions

---

# 🏢 Real Production Scenario

## CI/CD Deployment Architecture

```text
Developer

↓

GitHub

↓

GitHub Actions

↓

IAM Role (OIDC)

↓

AWS

↓

EC2

↓

Application Load Balancer

↓

Users
```

### How It Works

1. A developer pushes code to GitHub.
2. GitHub Actions authenticates to AWS using an IAM Role (via OIDC), avoiding long-lived access keys.
3. The workflow deploys the application to EC2 instances.
4. The Application Load Balancer distributes user traffic to healthy instances.

Benefits:

✔ No long-lived AWS credentials

✔ Secure deployments

✔ Least privilege access

✔ Easy credential rotation

---

# IAM Users vs IAM Roles

| Feature | IAM User | IAM Role |
|----------|----------|----------|
| Long-Term Credentials | Yes | No |
| Temporary Credentials | No | Yes |
| Used By | People & Apps | AWS Services & Federated Identities |
| Access Keys | Yes | Not Required |

---

# Interview Questions

### What is IAM?

IAM is an AWS service used to securely manage authentication and authorization for AWS resources.

---

### What is the difference between an IAM User and an IAM Role?

An IAM User has long-term credentials.

An IAM Role provides temporary credentials and is commonly used by AWS services or federated identities.

---

### Why is MFA important?

MFA provides an additional layer of security beyond a password.

---

### Can one IAM User belong to multiple Groups?

Yes.

---

### What is the Principle of Least Privilege?

Grant only the minimum permissions required to perform a task.

---

# Screenshot

```text
screenshots/

└── iam/

    ├── iam-overview.png
    ├── create-user.png
    ├── create-group.png
    ├── create-role.png
    ├── attach-policy.png
    ├── enable-mfa.png
    ├── aws-cli.png
    └── iam-complete-lab.png
```

---

# Official AWS References

- AWS Identity and Access Management User Guide
- IAM JSON Policy Reference
- AWS Security Best Practices
- AWS Well-Architected Framework
- AWS CLI Command Reference

---

# Quick Revision

```text
IAM → Identity & Access Management

User → Individual Identity

Group → Collection of Users

Role → Temporary Credentials

Policy → Permission Document

MFA → Extra Security Layer

Least Privilege → Minimum Required Access
```

---

# Skills Covered

✔ IAM Users

✔ IAM Groups

✔ IAM Roles

✔ IAM Policies

✔ MFA

✔ Access Keys

✔ AWS CLI Authentication

✔ CloudTrail Auditing

✔ Least Privilege

✔ Production AWS Security

---

# Status

AWS Identity and Access Management (IAM) Completed 🔐🚀
