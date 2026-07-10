# 🖥️ Amazon EC2 (Elastic Compute Cloud)

## Complete EC2 Guide for DevOps Engineers

Amazon Elastic Compute Cloud (Amazon EC2) is an AWS compute service that provides secure and scalable virtual servers called **instances**.

EC2 allows engineers to run applications without maintaining physical servers.

---

# 📌 What is Amazon EC2?

Amazon EC2 provides resizable compute capacity in the cloud.

Traditional:

User → Physical Server → OS → Application

Cloud:

User → EC2 Instance → OS → Application


EC2 belongs to:

Infrastructure as a Service (IaaS)

Because AWS manages:

- Physical servers
- Networking hardware
- Data centers
- Hardware availability


User manages:

- Operating System
- Packages
- Applications
- Security patches

---

# 🚀 Why DevOps Engineers Use EC2

EC2 is used for:

- Application hosting
- Web servers
- Backend APIs
- CI/CD tools
- Docker hosts
- Kubernetes worker nodes
- Monitoring tools
- Testing environments


Examples:

Jenkins Server

Docker Engine Host

Prometheus Server

Application Server

Database Server


---

# 🏗️ EC2 Architecture


```text
                 Users

                   |

              Internet

                   |

          Internet Gateway

                   |

             AWS VPC

                   |

          Security Group

                   |

            EC2 Instance

                   |

            EBS Storage


Monitoring:

CloudWatch

Security:

IAM
```

---

# 🔥 EC2 Important Components


# 1. EC2 Instance


An instance is a virtual machine running in AWS.


Contains:

- CPU
- Memory
- Network
- Storage
- Operating System


Example:

Ubuntu EC2 server running Nginx application.

---

# 2. Amazon Machine Image (AMI)


AMI is a template used to create EC2 instances.


AMI includes:

- Operating System
- Application software
- Configuration
- Storage mapping


Examples:

Ubuntu AMI

Amazon Linux AMI

Windows Server AMI


Flow:

AMI

 ↓

Launch

 ↓

EC2 Instance


---

# 3. Instance Types


Instance type decides hardware capacity.


Controls:

- vCPU
- RAM
- Network performance
- Storage performance


Example:

t2.micro

```text
CPU: 1 vCPU

Memory: 1GB
```


Common families:


## General Purpose

Examples:

t3

m5


Used for:

- Web servers
- Small applications


## Compute Optimized

Example:

c6


Used for:

- High CPU workloads


## Memory Optimized

Example:

r6


Used for:

- Databases
- Cache systems


## Storage Optimized


Used for:

- Big data
- High disk performance

---

# 4. EC2 Purchasing Options


## On Demand


Pay only while running.


Good for:

- Testing
- Development


---

## Reserved Instances


Commit usage.

Good for:

Production workloads


---

## Spot Instances


Unused AWS capacity at cheaper price.

Good for:

- Batch jobs
- Temporary workloads

---

# 5. EC2 Lifecycle


```text
Launch

  ↓

Pending

  ↓

Running

  ↓

Stopping

  ↓

Stopped

  ↓

Terminated
```

---

# 6. Key Pair Authentication


AWS uses key pairs for secure access.


Contains:

Private Key:

```text
.pem file
```

Public Key:

Stored inside EC2


SSH connection:


```bash
chmod 400 key.pem


ssh -i key.pem ubuntu@public-ip
```

---

# 7. Security Groups


Security Group works like EC2 firewall.


Controls:


Inbound Traffic

```text
Internet → EC2
```


Outbound Traffic

```text
EC2 → Internet
```


Common Rules:


|Port|Protocol|Purpose|
|-|-|-|
|22|SSH|Linux Login|
|80|HTTP|Website|
|443|HTTPS|Secure Website|
|3306|MYSQL|Database|


Example:


Allow SSH only from your IP:

```text
22

Your-IP/32
```

---

# 8. EC2 Storage


## EBS (Elastic Block Store)


Persistent block storage.


Used for:

- OS disk
- Application data
- Database storage


Example:


```text
EC2

 +

EBS Volume
```


---

## Instance Store


Temporary storage.


Data removed when instance stops.


Used for:

Temporary workloads.

---

# 9. Elastic IP Address


Problem:


EC2 public IP changes after stop/start.


Solution:


Elastic IP gives static public IP.


Used for:

Production servers.

---

# 10. EC2 User Data


User Data executes scripts automatically during first boot.


Example:


Install Nginx automatically:


```bash
#!/bin/bash


apt update -y


apt install nginx -y


systemctl start nginx


systemctl enable nginx
```


Flow:

Launch EC2

↓

Run Script

↓

Application Ready


---

# 11. IAM Role With EC2


Avoid storing AWS credentials inside servers.


Wrong:


```text
Access Key inside EC2
```


Correct:


```text
EC2

 ↓

IAM Role

 ↓

AWS Service Access
```


Example:


EC2 uploads files to S3 using IAM Role.

---

# 12. EC2 Monitoring


Amazon CloudWatch monitors:


- CPU usage
- Network traffic
- Status checks
- Logs
- Alarms


Example:


CPU > 80%

↓

CloudWatch Alarm

↓

SNS Notification

---

# 🚀 Launch EC2 Practical Steps


1. Open EC2 Console

2. Launch Instance

3. Select AMI

4. Choose Instance Type

5. Create Key Pair

6. Configure Network

7. Configure Security Group

8. Add Storage

9. Launch Instance

10. SSH Login


---

# 🧪 Practical Lab 1

Deploy Nginx Website


SSH:

```bash
ssh -i key.pem ubuntu@ip
```


Update:

```bash
sudo apt update
```


Install:

```bash
sudo apt install nginx -y
```


Check:

```bash
systemctl status nginx
```


Open:

```text
http://public-ip
```

---

# 🧪 Practical Lab 2

Create Web Server Using User Data


Add:


```bash
#!/bin/bash

apt update -y

apt install nginx -y

echo "AWS DevOps Project" > /var/www/html/index.html

systemctl start nginx
```

---

# AWS CLI Commands


List EC2:


```bash
aws ec2 describe-instances
```


Start:

```bash
aws ec2 start-instances \
--instance-ids INSTANCE-ID
```


Stop:

```bash
aws ec2 stop-instances \
--instance-ids INSTANCE-ID
```


Terminate:

```bash
aws ec2 terminate-instances \
--instance-ids INSTANCE-ID
```

---

# Production Best Practices


✔ Use IAM Roles

✔ Restrict SSH Access

✔ Enable CloudWatch

✔ Patch OS regularly

✔ Use Auto Scaling

✔ Take EBS snapshots

✔ Avoid hardcoded credentials

✔ Use private subnets for backend servers


---

# Common Troubleshooting


## SSH Permission Error


Fix:

```bash
chmod 400 key.pem
```


---

## Connection Timeout


Check:

Security Group

Route Table

Internet Gateway


---

## Website Down


Check:

```bash
systemctl status nginx


ss -tulnp


journalctl -u nginx
```

---

# Real DevOps Usage


EC2 is used with:

- Docker
- Kubernetes
- Jenkins
- Terraform
- Ansible
- Monitoring tools


---

# Skills Covered


✔ EC2 Administration

✔ Cloud Compute

✔ SSH Access

✔ Linux Server Management

✔ Security Groups

✔ IAM Integration

✔ Cloud Monitoring

✔ Production Troubleshooting
