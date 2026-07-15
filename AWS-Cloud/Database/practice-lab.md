# 🧪 AWS Database Practice Lab

# End-to-End Amazon RDS & Aurora Hands-on Lab

This lab combines everything learned in the Database section into one complete production-style deployment.

You will create:

- Amazon RDS MySQL
- Amazon Aurora Cluster
- DB Subnet Group
- Security Groups
- EC2 Database Client
- Read Replica
- Multi-AZ Deployment
- Performance Insights
- CloudWatch Monitoring
- Automated Backups
- Manual Snapshot
- Database Restore

By the end of this lab, you will understand how production databases are deployed, monitored, secured, backed up, and restored in AWS.

---

# 🎯 Lab Objectives

After completing this lab, you will be able to:

- Deploy Amazon RDS
- Deploy Amazon Aurora
- Configure networking
- Connect EC2 to databases
- Enable monitoring
- Configure backups
- Restore databases
- Test failover
- Monitor performance

---

# Architecture

```text
                     Internet

                         │

                Application Load Balancer

                         │

                 Amazon EC2 Client

                         │

                 Security Group

                         │

            Amazon Aurora Cluster

                         │

         ┌───────────────┼───────────────┐

         │                               │

   Writer Instance               Reader Instance

                         │

              Shared Distributed Storage

                         │

              Performance Insights

                         │

                 Amazon CloudWatch

                         │

                    Amazon SNS
```

---

# Prerequisites

Before starting, make sure you already have:

- AWS Account
- VPC
- Public Subnet
- Private Subnets (2)
- Internet Gateway
- NAT Gateway
- Security Groups
- EC2 Instance
- IAM Permissions

---

# Part 1 – Create DB Subnet Group

Go to:

```text
AWS Console

↓

Amazon RDS

↓

Subnet Groups

↓

Create DB Subnet Group
```

Configuration

```text
Name

database-subnet-group

VPC

Your VPC

Availability Zones

2

Private Subnets

2
```

Expected Result

✅ DB Subnet Group Created

---

# Part 2 – Create Amazon RDS

Navigate to

```text
Amazon RDS

↓

Create Database
```

Configuration

```text
Engine

MySQL

Template

Free Tier

DB Identifier

production-db

Master Username

admin

Storage

20 GB gp3

Multi-AZ

Disabled

Public Access

No

Performance Insights

Enabled

Backup Retention

7 Days
```

Expected Result

✅ Amazon RDS Available

---

# Part 3 – Configure Security Group

Inbound Rule

```text
Type

MySQL/Aurora

Port

3306

Source

EC2 Security Group
```

Expected Result

✅ EC2 Can Access Database

---

# Part 4 – Connect EC2 to RDS

SSH into EC2

```bash
ssh -i key.pem ec2-user@PUBLIC_IP
```

Install MySQL Client

Amazon Linux

```bash
sudo yum install mariadb105 -y
```

Ubuntu

```bash
sudo apt update
sudo apt install mysql-client -y
```

Connect

```bash
mysql -h RDS_ENDPOINT \
-u admin \
-p
```

Expected Result

```text
mysql>
```

---

# Part 5 – Create Database

```sql
CREATE DATABASE company;
```

Use Database

```sql
USE company;
```

Create Table

```sql
CREATE TABLE employees(
id INT PRIMARY KEY,
name VARCHAR(50),
department VARCHAR(50)
);
```

Insert Data

```sql
INSERT INTO employees VALUES
(1,'John','DevOps'),
(2,'Alice','Cloud');
```

Verify

```sql
SELECT * FROM employees;
```

Expected Result

```text
2 rows returned
```

---

# Part 6 – Enable Multi-AZ

Modify Database

```text
Amazon RDS

↓

Modify

↓

Enable Multi-AZ

↓

Apply Immediately
```

Expected Result

✅ Standby Database Created

---

# Part 7 – Create Read Replica

```text
Actions

↓

Create Read Replica
```

Configuration

```text
Replica Name

production-read

Instance Class

db.t3.micro
```

Expected Result

✅ Read Replica Available

---

# Part 8 – Enable CloudWatch Monitoring

Open

```text
CloudWatch

↓

Metrics

↓

RDS
```

Monitor

- CPU
- Free Storage
- Connections
- Read IOPS
- Write IOPS

Create Dashboard

```text
Database Dashboard
```

Expected Result

✅ Dashboard Created

---

# Part 9 – Enable Performance Insights

Navigate

```text
Amazon RDS

↓

Performance Insights
```

Observe

- Database Load
- Top SQL
- Wait Events
- Active Sessions

Expected Result

✅ Performance Dashboard Visible

---

# Part 10 – Create Manual Snapshot

Navigate

```text
Amazon RDS

↓

Snapshots

↓

Take Snapshot
```

Snapshot Name

```text
production-backup
```

Expected Result

✅ Snapshot Created

---

# Part 11 – Restore Snapshot

Navigate

```text
Snapshots

↓

production-backup

↓

Restore Snapshot
```

Database Name

```text
restored-db
```

Expected Result

✅ Database Restored

---

# Part 12 – Create Aurora Cluster

Navigate

```text
Amazon RDS

↓

Create Database

↓

Amazon Aurora
```

Configuration

```text
Engine

Aurora MySQL

Cluster Name

production-cluster

Writer

1

Reader

1

Performance Insights

Enabled
```

Expected Result

✅ Aurora Cluster Running

---

# Part 13 – Connect to Aurora

```bash
mysql \
-h CLUSTER_ENDPOINT \
-u admin \
-p
```

Expected Result

```text
Connected Successfully
```

---

# Part 14 – Test Failover

Navigate

```text
Amazon RDS

↓

Aurora Cluster

↓

Failover
```

Observe

- Writer Changes
- Cluster Endpoint Remains Same
- Application Continues Running

Expected Result

✅ Automatic Failover Successful

---

# Part 15 – Cleanup

Delete

- Aurora Cluster
- Read Replica
- RDS Instance
- Snapshots (optional)
- DB Subnet Group

Expected Result

✅ Resources Deleted

---

# Validation Checklist

| Task | Status |
|-------|--------|
| DB Subnet Group Created | ⬜ |
| Amazon RDS Created | ⬜ |
| Security Group Configured | ⬜ |
| EC2 Connected | ⬜ |
| Database Created | ⬜ |
| Multi-AZ Enabled | ⬜ |
| Read Replica Created | ⬜ |
| CloudWatch Monitoring Enabled | ⬜ |
| Performance Insights Enabled | ⬜ |
| Snapshot Created | ⬜ |
| Snapshot Restored | ⬜ |
| Aurora Cluster Created | ⬜ |
| Aurora Connected | ⬜ |
| Failover Tested | ⬜ |
| Resources Cleaned Up | ⬜ |

---

# Skills Practiced

✔ Amazon RDS

✔ Amazon Aurora

✔ MySQL Administration

✔ DB Subnet Groups

✔ Security Groups

✔ Multi-AZ

✔ Read Replicas

✔ Performance Insights

✔ CloudWatch Monitoring

✔ Manual Snapshots

✔ Automated Backups

✔ Database Restore

✔ Failover Testing

✔ Disaster Recovery

---

# Lab Outcome

After completing this lab, you will have hands-on experience with:

- Deploying production-ready relational databases
- Securing database connectivity
- Monitoring performance
- Scaling read workloads
- Configuring high availability
- Backing up and restoring databases
- Performing failover testing
- Applying AWS database best practices

---

# Status

🎉 AWS Database Practice Lab Completed Successfully 🚀
