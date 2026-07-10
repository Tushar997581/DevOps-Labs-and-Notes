# 📈 Amazon EC2 Auto Scaling for DevOps Engineers

## Complete Auto Scaling Guide

Amazon EC2 Auto Scaling automatically adjusts the number of EC2 instances based on application demand.

It helps maintain application availability, improves performance, and reduces unnecessary cost.

---

# 📌 What is Auto Scaling?

Auto Scaling automatically:

- Adds EC2 instances when traffic increases
- Removes EC2 instances when traffic decreases
- Maintains required server capacity
- Replaces unhealthy instances


Example:

```text
Normal Traffic:

2 EC2 Instances


High Traffic:

Auto Scaling Adds More Instances


Low Traffic:

Auto Scaling Removes Extra Instances
```

---

# 🚀 Why DevOps Engineers Use Auto Scaling?

Auto Scaling helps with:

✔ High Availability  
✔ Fault Tolerance  
✔ Cost Optimization  
✔ Automatic Recovery  
✔ Handling Traffic Spikes  


Real examples:

- E-commerce sales
- Streaming applications
- Production APIs
- High traffic websites

---

# 🏗️ Auto Scaling Architecture


```text
                    Users

                      |

                      ↓

          Application Load Balancer

                      |

          -----------------------

          |                     |

       EC2 Instance         EC2 Instance


                      |

                      ↓


             Auto Scaling Group


                      |

              Launch Template


Monitoring:

CloudWatch Metrics

        ↓

Scaling Policies
```

---

# 🔥 Auto Scaling Components


# 1. Launch Template


Launch Template defines how new EC2 instances are created.


Contains:

- AMI
- Instance Type
- Key Pair
- Security Group
- User Data
- Storage configuration


Example:


```text
Launch Template

        ↓

Ubuntu AMI

t2.micro

Security Group

User Data Script

        ↓

New EC2 Instance
```

---

# 2. Auto Scaling Group (ASG)


ASG manages EC2 instances.


Controls:

- How many instances run
- Where instances run
- Health replacement


Important values:

```text
Minimum Capacity

Desired Capacity

Maximum Capacity
```


Example:

```text
Minimum: 2

Desired: 2

Maximum: 6
```


Meaning:

Always keep 2 servers.

Scale maximum up to 6 servers.

---

# 3. Scaling Policy


Defines when scaling happens.


Example:


```text
CPU > 70%

        ↓

Add EC2 Instance
```


```text
CPU < 30%

        ↓

Remove EC2 Instance
```

---

# 4. CloudWatch Metrics


CloudWatch monitors EC2 performance.


Common metrics:

- CPU Utilization
- Network Usage
- Request Count
- Memory (with agent)


CloudWatch triggers scaling actions.

---

# 5. Elastic Load Balancer Integration


Auto Scaling works with Load Balancer.


Flow:


```text
User Request

↓

Load Balancer

↓

Healthy EC2 Instances

↓

Application Response
```


Benefits:

- Traffic distribution
- Removes unhealthy servers
- Better availability

---

# 📊 Types of Scaling


# 1. Dynamic Scaling


Automatically changes capacity.


Example:


CPU increases → Add instance


CPU decreases → Remove instance


---

# 2. Scheduled Scaling


Scaling based on time.


Example:


```text
9 AM

Increase servers


10 PM

Reduce servers
```


Useful when traffic pattern is predictable.

---

# 3. Predictive Scaling


AWS predicts future traffic using machine learning.


Example:


Traffic increases every Monday.


AWS scales before traffic arrives.

---

# ⚙️ Scaling Policies


## Target Tracking Scaling


Maintain target value.


Example:


```text
Keep CPU around 50%
```


AWS automatically adjusts instances.

---

## Step Scaling


Scale based on different levels.


Example:


```text
CPU 70%

+1 Instance


CPU 90%

+3 Instances
```

---

# 🧪 Practical Lab 1

## Create Auto Scaling Web Application


Goal:

Deploy highly available Nginx servers.


Architecture:


```text
ALB

 ↓

Auto Scaling Group

 ↓

EC2 Instances
```

---

# Step 1: Create Launch Template


Configuration:


```text
AMI:

Ubuntu


Instance:

t2.micro


Security:

Allow HTTP 80
```

---

# Step 2: Add User Data


Install Nginx automatically:


```bash
#!/bin/bash


apt update -y


apt install nginx -y


echo "AWS Auto Scaling Demo" > /var/www/html/index.html


systemctl start nginx
```

---

# Step 3: Create Auto Scaling Group


Set:


```text
Minimum instances: 2

Desired instances: 2

Maximum instances: 5
```

---

# Step 4: Attach Load Balancer


Create:


```text
Application Load Balancer


Target Group


Attach ASG
```

---

# Step 5: Test Scaling


Install stress tool:


```bash
sudo apt install stress -y
```


Increase CPU:


```bash
stress --cpu 2 --timeout 300
```


CloudWatch detects load and scales.

---

# AWS CLI Commands


Describe Auto Scaling Groups:


```bash
aws autoscaling describe-auto-scaling-groups
```


Update capacity:


```bash
aws autoscaling update-auto-scaling-group \
--auto-scaling-group-name my-asg \
--desired-capacity 3
```

---

# 🔥 Auto Scaling Troubleshooting


## Instances Not Launching


Check:

- Launch Template
- AMI ID
- IAM permissions
- Instance limits


---

# Instance Failing Health Check


Check:

```bash
systemctl status nginx
```


Verify:

- Security Group
- Target Group health checks

---

# Scaling Not Triggering


Check:

- CloudWatch Alarm
- Scaling Policy
- Metric threshold

---

# 🔐 Best Practices


✔ Use multiple Availability Zones

✔ Attach Load Balancer

✔ Configure health checks

✔ Use Launch Templates

✔ Enable CloudWatch monitoring

✔ Avoid fixed capacity

✔ Use IAM roles

✔ Test scaling events


---

# Auto Scaling vs Load Balancer


| Auto Scaling | Load Balancer |
|-|-|
|Adds/removes EC2|Distributes traffic|
|Capacity control|Traffic control|
|Uses CloudWatch|Uses Target Groups|
|Improves availability|Improves reliability|

---

# 🎯 DevOps Use Cases


Auto Scaling is used for:

✔ Production web apps  
✔ Microservices  
✔ High traffic systems  
✔ Cost optimization  
✔ Disaster recovery  
✔ Cloud automation  


---

# 🚀 Skills Covered


- EC2 Auto Scaling
- Launch Templates
- Scaling Policies
- CloudWatch Integration
- Load Balancer Architecture
- High Availability Design
- Production Scaling
