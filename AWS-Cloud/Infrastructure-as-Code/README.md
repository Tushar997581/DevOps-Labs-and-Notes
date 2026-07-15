# 🏗️ Infrastructure as Code (IaC)

# Complete Terraform Guide for DevOps Engineers

Modern cloud infrastructure is no longer created manually through web consoles. Instead, infrastructure is defined using code, making deployments repeatable, scalable, version-controlled, and automated.

Infrastructure as Code (IaC) is one of the most important DevOps practices. It allows engineers to provision and manage infrastructure using configuration files instead of manual operations.

In this section, you will learn Infrastructure as Code using **Terraform**, the industry-leading IaC tool developed by HashiCorp.

---

# 🎯 Learning Objectives

After completing this section, you will be able to:

- Understand Infrastructure as Code (IaC)
- Install and configure Terraform
- Write Terraform configuration files
- Deploy AWS infrastructure using Terraform
- Manage Terraform State
- Use Variables and Outputs
- Create reusable Modules
- Configure Remote State
- Use Workspaces
- Build production-ready AWS infrastructure
- Follow Terraform best practices

---

# 📖 What is Infrastructure as Code (IaC)?

Infrastructure as Code (IaC) is the process of managing and provisioning infrastructure using code instead of manual configuration.

Instead of creating AWS resources through the AWS Management Console, you write configuration files that describe the desired infrastructure.

Example:

Without IaC

```text
Login AWS Console

↓

Create VPC

↓

Create Subnets

↓

Create Security Groups

↓

Create EC2

↓

Launch Application
```

With IaC

```text
Terraform Code

↓

terraform apply

↓

AWS Infrastructure Created
```

The infrastructure becomes repeatable, consistent, and easy to manage.

---

# Why Infrastructure as Code?

Imagine you have to create the same infrastructure five times.

Without IaC

```text
Developer 1

↓

Clicks AWS Console

↓

Creates Resources

↓

Developer 2

↓

Creates Different Resources
```

Problems

❌ Human Errors

❌ Inconsistent Infrastructure

❌ Slow Deployment

❌ Difficult Scaling

❌ No Version Control

---

With Terraform

```text
Terraform Configuration

↓

Git Repository

↓

terraform apply

↓

Identical Infrastructure
```

Benefits

✔ Automation

✔ Repeatability

✔ Version Control

✔ Faster Deployment

✔ Consistency

✔ Collaboration

---

# What is Terraform?

Terraform is an open-source Infrastructure as Code (IaC) tool developed by HashiCorp.

Terraform allows you to create, modify, and manage cloud infrastructure using declarative configuration files written in **HashiCorp Configuration Language (HCL)**.

Terraform supports hundreds of providers including:

- AWS
- Microsoft Azure
- Google Cloud Platform (GCP)
- Kubernetes
- Docker
- GitHub
- Cloudflare
- VMware

---

# Terraform Architecture

```text
            Terraform Code

                  │

          terraform init

                  │

          Terraform Provider

                  │

          AWS API Requests

                  │

          AWS Infrastructure
```

---

# How Terraform Works

Terraform follows a simple workflow.

```text
Write Code

↓

Initialize

↓

Plan

↓

Apply

↓

Infrastructure Created
```

---

# Terraform Workflow

## Step 1 – Write Configuration

Create Terraform files.

```text
main.tf

variables.tf

outputs.tf
```

---

## Step 2 – Initialize

```bash
terraform init
```

Terraform downloads the required providers.

---

## Step 3 – Validate

```bash
terraform validate
```

Checks configuration syntax and validates references.

---

## Step 4 – Format

```bash
terraform fmt
```

Formats Terraform files according to standard style.

---

## Step 5 – Plan

```bash
terraform plan
```

Shows what Terraform will create, update, or delete.

---

## Step 6 – Apply

```bash
terraform apply
```

Creates or updates infrastructure.

---

## Step 7 – Destroy

```bash
terraform destroy
```

Removes infrastructure managed by Terraform.

---

# Terraform Lifecycle

```text
Write Code

↓

Init

↓

Validate

↓

Plan

↓

Apply

↓

Infrastructure Running

↓

Modify Code

↓

Plan

↓

Apply

↓

Updated Infrastructure

↓

Destroy
```

---

# Terraform File Structure

A typical project looks like this:

```text
terraform-project/

├── main.tf
├── provider.tf
├── variables.tf
├── outputs.tf
├── terraform.tfvars
├── versions.tf
└── terraform.tfstate
```

As projects grow, modules and additional directories are commonly introduced.

---

# HashiCorp Configuration Language (HCL)

Terraform configurations are written in HCL.

Example:

```hcl
resource "aws_instance" "web" {
  ami           = "ami-xxxxxxxx"
  instance_type = "t2.micro"
}
```

HCL is designed to be human-readable and declarative.

---

# Terraform Providers

Providers enable Terraform to interact with external platforms.

Examples:

```text
AWS Provider

↓

Create EC2

Create VPC

Create S3

Create IAM
```

Other providers include:

- Azure
- Google Cloud
- Kubernetes
- Docker
- GitHub

---

# Terraform Resources

Resources represent infrastructure components.

Examples:

- VPC
- EC2
- S3 Bucket
- IAM User
- Security Group
- Route Table

Example:

```text
Terraform Resource

↓

AWS EC2 Instance
```

---

# Terraform State

Terraform stores infrastructure information in a **State File**.

```text
terraform.tfstate
```

The state file maps Terraform configuration to real infrastructure.

Terraform uses this file to determine what changes are required.

---

# Remote State

Production environments should store the state remotely.

Example:

```text
Terraform

↓

Amazon S3

↓

terraform.tfstate

↓

DynamoDB

↓

State Locking
```

Benefits

✔ Team Collaboration

✔ Secure Storage

✔ State Locking

✔ Disaster Recovery

---

# Terraform Modules

Modules allow infrastructure to be reused.

Example

```text
Network Module

↓

VPC

Subnets

Internet Gateway

Route Tables
```

Benefits

✔ Reusability

✔ Standardization

✔ Easier Maintenance

---

# Terraform Workspaces

Workspaces allow multiple environments using the same configuration.

Example

```text
Development

↓

Testing

↓

Production
```

Each workspace has its own state.

---

# Terraform vs AWS CloudFormation

| Feature | Terraform | AWS CloudFormation |
|----------|-----------|--------------------|
| Developer | HashiCorp | AWS |
| Cloud Support | Multi-Cloud | AWS Only |
| Language | HCL | JSON / YAML |
| Open Source | Yes | No |
| Community | Very Large | AWS Ecosystem |
| State File | Yes | Managed by AWS |

---

# Production Architecture

```text
              Git Repository

                     │

             Terraform Code

                     │

            GitHub Actions / CI

                     │

             terraform init

                     │

             terraform plan

                     │

             terraform apply

                     │

             AWS Provider

                     │

      ┌──────────────┼──────────────┐

      │              │              │

     VPC            EC2            RDS

      │              │              │

      └──────────────┼──────────────┘

                     │

               AWS Infrastructure
```

---

# DevOps Use Cases

Terraform is commonly used for:

✔ VPC Deployment

✔ EC2 Provisioning

✔ Kubernetes Clusters

✔ IAM Management

✔ S3 Buckets

✔ Auto Scaling

✔ Load Balancers

✔ RDS Databases

✔ Complete Cloud Infrastructure

---

# Best Practices

✔ Use Modules

✔ Store State Remotely

✔ Enable State Locking

✔ Use Variables

✔ Keep Secrets out of Code

✔ Commit Code to Git

✔ Review `terraform plan` before applying

✔ Follow consistent naming conventions

✔ Organize projects by environment

✔ Pin provider versions where appropriate

---

# Projects Included

## Project 1

Deploy a Complete AWS VPC

---

## Project 2

Deploy a Production EC2 Infrastructure

---

## Project 3

Deploy a Three-Tier Application

---

## Project 4

Remote State Management using Amazon S3 and DynamoDB

---

## Project 5

Build Reusable Terraform Modules

---

# Skills You Will Gain

After completing this section you will understand:

✔ Infrastructure as Code

✔ Terraform Fundamentals

✔ Providers

✔ Resources

✔ Variables

✔ Outputs

✔ Modules

✔ Remote State

✔ Workspaces

✔ Production Infrastructure

---

# Learning Path

```text
06-Infrastructure-as-Code/

│

├── README

├── Terraform

├── Installation

├── Providers

├── Resources

├── Variables

├── Outputs

├── Locals

├── Data Sources

├── State Management

├── Remote State

├── Modules

├── Workspaces

├── Provisioners

├── Lifecycle

├── Functions

├── Import

├── Taint & Replace

├── Fmt & Validate

├── Plan, Apply & Destroy

├── Projects

├── Practice Lab

└── Screenshots
```

---

# Official References

- HashiCorp Terraform Documentation
- Terraform Language Documentation
- Terraform AWS Provider Documentation
- Terraform CLI Documentation
- AWS Well-Architected Framework

---

# Repository Structure

```text
06-Infrastructure-as-Code/

├── README.md
├── terraform.md
├── installation.md
├── providers.md
├── resources.md
├── variables.md
├── outputs.md
├── locals.md
├── data-sources.md
├── state-management.md
├── remote-state.md
├── modules.md
├── workspaces.md
├── provisioners.md
├── lifecycle.md
├── functions.md
├── import.md
├── taint-replace.md
├── fmt-validate.md
├── plan-apply-destroy.md
├── projects.md
├── practice-lab.md
└── screenshots/
```

---

# Status

🏗️ Infrastructure as Code (Terraform) Section Started 🚀
