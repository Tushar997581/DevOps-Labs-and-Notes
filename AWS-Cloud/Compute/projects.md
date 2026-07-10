# 🚀 AWS Compute Real-World Projects

## Production-Level AWS Compute Implementations for DevOps Engineers

This section contains hands-on projects using AWS Compute services.

The goal is to understand how EC2, Lambda, Auto Scaling, and Elastic Beanstalk work together in real production environments.

---

# Project 01: Highly Available Web Application Using EC2 & Auto Scaling

## 📌 Project Overview

Deploy a scalable and highly available web application infrastructure on AWS.

The application automatically handles traffic changes using EC2 Auto Scaling and distributes requests using a Load Balancer.

---

# 🏗️ Architecture


```text
                 Users

                   |

                   ↓

          Application Load Balancer

                   |

        -----------------------

        |                     |

 Availability Zone A     Availability Zone B

        |                     |

      EC2                  EC2

        \                   /

         \                 /

          Auto Scaling Group


Monitoring:

CloudWatch

Alerts:

SNS


Security:

IAM + Security Groups
```

---

# ☁️ AWS Services Used


| Service | Purpose |
|-|-|
| EC2 | Application servers |
| Auto Scaling | Automatic capacity management |
| Load Balancer | Traffic distribution |
| IAM | Secure permissions |
| CloudWatch | Monitoring |
| SNS | Notifications |
| VPC | Network isolation |


---

# Implementation Steps


## Step 1: Create Launch Template


Configure:

```text
AMI:

Ubuntu


Instance Type:

t2.micro


Security Group:

HTTP 80

SSH 22
```

---

# Step 2: Add User Data


Install web server automatically:


```bash
#!/bin/bash


apt update -y


apt install nginx -y


echo "AWS Compute Project" \
> /var/www/html/index.html


systemctl enable nginx


systemctl start nginx
```

---

# Step 3: Create Auto Scaling Group


Configuration:


```text
Minimum Capacity: 2

Desired Capacity: 2

Maximum Capacity: 5
```

---

# Step 4: Configure Load Balancer


Create:

```text
Application Load Balancer

        |

Target Group

        |

EC2 Instances
```

---

# Step 5: Configure Scaling Policy


Example:


```text
CPU > 70%

      ↓

Add EC2 Instance
```

---

# Step 6: Setup Monitoring


CloudWatch:

Monitor:

- CPU usage
- Instance health
- Network traffic


SNS:

Send alert notifications.

---

# Testing


Generate CPU load:


```bash
sudo apt install stress -y


stress --cpu 2 --timeout 300
```


Expected:

```text
Traffic Increase

↓

CloudWatch Alarm

↓

Auto Scaling Adds Instance
```

---

# Skills Learned


✔ EC2 Deployment  
✔ Load Balancing  
✔ High Availability  
✔ Auto Scaling  
✔ Monitoring  
✔ Production Architecture  


---

<br>

# Project 02: Serverless EC2 Automation Using AWS Lambda


## 📌 Project Overview


Create a serverless automation system to automatically manage EC2 instances.


Example:

Automatically stop development servers after working hours.

---

# Architecture


```text
              EventBridge

                   |

                   ↓

              AWS Lambda

                   |

                   ↓

              EC2 Instances


Logs:

CloudWatch
```

---

# AWS Services Used


|Service|Purpose|
|-|-|
|Lambda|Automation logic|
|EC2|Target servers|
|IAM Role|Permissions|
|EventBridge|Scheduling|
|CloudWatch|Logs|

---

# Implementation


## Step 1: Create IAM Role


Required permissions:


```json
{
 "Action":[

 "ec2:StartInstances",

 "ec2:StopInstances"

 ],

 "Effect":"Allow",

 "Resource":"*"
}
```

---

# Step 2: Create Lambda Function


Runtime:

```text
Python
```

---

# Lambda Code


Stop EC2:


```python
import boto3


ec2=boto3.client("ec2")


def lambda_handler(event, context):


    ec2.stop_instances(

    InstanceIds=[

    "INSTANCE-ID"

    ]

    )


    return "Instance stopped"
```

---

# Step 3: Create EventBridge Schedule


Example:


```text
Every day

8 PM

↓

Trigger Lambda
```

---

# Step 4: Monitor Logs


Check:


```text
CloudWatch

↓

Log Groups

↓

Lambda Logs
```

---

# Skills Learned


✔ Serverless Automation  
✔ Lambda Functions  
✔ IAM Roles  
✔ AWS SDK (Boto3)  
✔ CloudWatch Logs  
✔ Cost Optimization  


---

<br>


# Project 03: Application Deployment Using Elastic Beanstalk


## Project Goal


Deploy application without manually managing infrastructure.


---

# Architecture


```text
Developer

↓

Application Code

↓

Elastic Beanstalk

↓

Load Balancer

↓

EC2 Auto Scaling
```

---

# Steps


Install EB CLI:


```bash
pip install awsebcli
```


Initialize:


```bash
eb init
```


Create environment:


```bash
eb create production
```


Deploy:


```bash
eb deploy
```

---

# Deployment Strategies Covered


- Rolling Deployment
- Immutable Deployment
- Application Versioning
- Rollback


---

# Repository Evidence Checklist


Add screenshots:


```text
screenshots/compute-projects/


├── ec2-running.png

├── load-balancer.png

├── auto-scaling.png

├── lambda-execution.png

├── cloudwatch-logs.png

└── elastic-beanstalk.png
```

---

# Resume Description


AWS Compute Projects:

Designed and implemented scalable cloud infrastructure using Amazon EC2, Auto Scaling Groups, Elastic Load Balancing, Lambda automation, IAM roles, and CloudWatch monitoring.

---

# Concepts Practiced


✔ Infrastructure Scalability  
✔ Serverless Automation  
✔ High Availability Design  
✔ Production Deployment  
✔ Cloud Monitoring  
✔ AWS Security Practices  


---

# Status

AWS Compute Projects Completed 🚀

Next Section:

💾 AWS Storage & Content Delivery
