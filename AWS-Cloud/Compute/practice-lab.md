# 🧪 AWS Compute Practical Labs for DevOps Engineers

This lab contains real-world hands-on AWS Compute exercises.

The goal is to practice EC2 administration, serverless automation, auto scaling infrastructure, and application deployment workflows used in production environments.

---

# 🛠️ Lab Environment

Services Used:

- Amazon EC2
- AWS Lambda
- EC2 Auto Scaling
- Elastic Beanstalk
- IAM
- CloudWatch
- Security Groups
- AWS CLI

---

# 🧪 Lab 1: Launch EC2 Linux Server

## Goal

Create and access a Linux cloud server.

Architecture:

```text
User

 ↓

SSH

 ↓

Security Group

 ↓

EC2 Instance

 ↓

EBS Volume
```

---

## Step 1: Launch Instance


Configuration:

```text
AMI:

Ubuntu Linux


Instance Type:

t2.micro


Storage:

8GB EBS
```

---

## Step 2: Security Group


Allow:

```text
SSH

Port: 22

Source: Your IP
```

---

## Step 3: Connect Using SSH


Set permission:

```bash
chmod 400 devops-key.pem
```


Connect:

```bash
ssh -i devops-key.pem ubuntu@PUBLIC_IP
```

---

# 🧪 Lab 2: Deploy Website on EC2


Install Nginx:

```bash
sudo apt update


sudo apt install nginx -y
```


Start service:

```bash
sudo systemctl start nginx
```


Enable:

```bash
sudo systemctl enable nginx
```


Create webpage:

```bash
echo "AWS EC2 DevOps Lab" \
| sudo tee /var/www/html/index.html
```


Open:

```text
http://EC2_PUBLIC_IP
```

---

# 🧪 Lab 3: EC2 User Data Automation


Goal:

Automatically configure server during launch.


Add User Data:


```bash
#!/bin/bash


apt update -y


apt install nginx -y


echo "Automated EC2 Deployment" > /var/www/html/index.html


systemctl start nginx


systemctl enable nginx
```


Result:

```text
Launch EC2

     ↓

Script Executes

     ↓

Website Ready
```

---

# 🧪 Lab 4: EC2 Monitoring Using CloudWatch


Monitor:

- CPU Utilization
- Network Traffic
- Status Checks


Steps:

```text
EC2 Console

↓

Monitoring

↓

CloudWatch Metrics
```

---

Create Alarm:

Example:

```text
Condition:

CPU > 80%

Action:

Send Alert
```

---

# 🧪 Lab 5: Create Lambda Function


Goal:

Run serverless code.


Create:

```text
Lambda

↓

Create Function

↓

Python Runtime
```

---

Code:

```python
def lambda_handler(event, context):

    return {

    "message":"Hello AWS Lambda"

    }
```

---

Test:

Expected:

```json
{
"message":"Hello AWS Lambda"
}
```

---

# 🧪 Lab 6: Lambda EC2 Automation


Architecture:

```text
EventBridge

     ↓

Lambda

     ↓

EC2 Start/Stop
```

---

IAM Permission Required:

```text
ec2:StartInstances

ec2:StopInstances
```

---

Python:

```python
import boto3


ec2=boto3.client("ec2")


def lambda_handler(event,context):


    ec2.stop_instances(

    InstanceIds=["INSTANCE_ID"]

    )
```

---

# 🧪 Lab 7: Create Auto Scaling Architecture


Goal:

Highly available web servers.


Architecture:

```text
Users

 ↓

Application Load Balancer

 ↓

Auto Scaling Group

 ↓

EC2 Instances
```

---

Create:

1. Launch Template

2. Auto Scaling Group

3. Target Group

4. Load Balancer

5. Scaling Policy


---

Capacity:

```text
Minimum:

2


Desired:

2


Maximum:

5
```

---

# Test Auto Scaling


Install stress:

```bash
sudo apt install stress -y
```


Increase CPU:

```bash
stress --cpu 2 --timeout 300
```


Result:

```text
CPU Increase

↓

CloudWatch Alarm

↓

New EC2 Created
```

---

# 🧪 Lab 8: Deploy App Using Elastic Beanstalk


Install EB CLI:

```bash
pip install awsebcli
```

---

Initialize:

```bash
eb init
```

---

Create Environment:

```bash
eb create dev-env
```

---

Deploy:

```bash
eb deploy
```

---

Check:

```bash
eb status
```

---

# 🧪 Lab 9: AWS CLI Practice


Check EC2:

```bash
aws ec2 describe-instances
```


Check Lambda:

```bash
aws lambda list-functions
```


Check Auto Scaling:

```bash
aws autoscaling describe-auto-scaling-groups
```

---

# 🔥 Troubleshooting Practice


## EC2 SSH Failed


Check:

✔ Security Group  
✔ Key Permission  
✔ Public IP  
✔ Route Table  


Fix:

```bash
chmod 400 key.pem
```

---

## Lambda Permission Error


Issue:

```text
AccessDenied
```


Fix:

Check:

```text
IAM Execution Role
```

---

## Auto Scaling Not Working


Verify:

- CloudWatch Alarm
- Scaling Policy
- Launch Template

---

# 📸 Screenshot Checklist


Add:

```text
screenshots/compute/

├── 01-ec2-running.png

├── 02-ssh-login.png

├── 03-nginx-website.png

├── 04-cloudwatch-monitoring.png

├── 05-lambda-function.png

├── 06-auto-scaling-group.png

└── 07-elastic-beanstalk.png
```

---

# 🎯 Real DevOps Skills Practiced


✔ Linux Server Deployment  
✔ Cloud Automation  
✔ Serverless Functions  
✔ Scaling Infrastructure  
✔ Application Deployment  
✔ Monitoring & Troubleshooting  


---

# 🚀 Compute Labs Completed

AWS Compute foundation successfully practiced for real-world DevOps environments.
