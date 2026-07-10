# ☁️ AWS Compute Services

## Complete AWS Compute Guide for DevOps Engineers

AWS Compute services provide the processing power required to build, deploy, run, and scale applications in the cloud.

Compute is one of the core foundations of cloud computing and is heavily used by DevOps Engineers for:

- Application hosting
- Automation
- Serverless workloads
- Container platforms
- CI/CD environments
- High availability systems

---

# 📌 What is Cloud Computing Compute?

In traditional infrastructure:

```text
Company

   ↓

Buy Physical Servers

   ↓

Install OS

   ↓

Configure Network

   ↓

Deploy Application

   ↓

Maintain Hardware
```

AWS Compute:

```text
Developer / DevOps Engineer

            ↓

        AWS Compute

            ↓

 Virtual Servers / Functions

            ↓

      Application Running
```

AWS manages:

✔ Data Centers  
✔ Physical Servers  
✔ Hardware  
✔ Infrastructure Availability


Users manage:

✔ Applications  
✔ Configuration  
✔ Security  
✔ Deployment  

---

# 🏗️ AWS Compute Architecture Overview


```text
                   Users

                     |

                     ↓

              AWS Compute Layer


 ------------------------------------------------

 |                    |                         |

EC2                Lambda              Elastic Beanstalk


Virtual           Serverless             Managed App

Servers           Functions              Platform


                     |

              Auto Scaling

                     |

        Automatic Capacity Management
```

---

# 🚀 Compute Services Covered


## 1. 🖥️ Amazon EC2  
(Elastic Compute Cloud)


EC2 provides scalable virtual machines in AWS.


Used for:

- Web servers
- Backend applications
- Docker hosts
- Kubernetes nodes
- Jenkins servers
- Databases


Important Topics:

- Instances
- AMI
- Instance Types
- Key Pairs
- Security Groups
- User Data
- IAM Roles
- CloudWatch Monitoring


Learn:

➡️ [Amazon EC2](./ec2.md)


---

# 2. ⚡ AWS Lambda


AWS Lambda is a serverless compute service.

Run code without managing servers.


Used for:

- Automation scripts
- Event processing
- Backend APIs
- Scheduled jobs
- AWS operations


Important Topics:

- Functions
- Runtime
- Handler
- Events
- Triggers
- Execution Role
- CloudWatch Logs


Learn:

➡️ [AWS Lambda](./lambda.md)


---

# 3. 📈 Amazon EC2 Auto Scaling


Auto Scaling automatically adjusts EC2 capacity according to application demand.


Used for:

- High availability
- Traffic handling
- Cost optimization
- Fault tolerance


Important Topics:

- Auto Scaling Groups
- Launch Templates
- Scaling Policies
- Health Checks
- CloudWatch Metrics


Learn:

➡️ [Auto Scaling](./auto-scaling.md)


---

# 4. 🌱 AWS Elastic Beanstalk


Elastic Beanstalk is a Platform as a Service (PaaS) solution for deploying applications.


AWS manages:

- EC2 creation
- Load Balancing
- Scaling
- Deployment


Used for:

- Web applications
- APIs
- Docker apps
- Rapid deployments


Important Topics:

- Application
- Environment
- Platform
- Deployment Strategies
- Monitoring


Learn:

➡️ [Elastic Beanstalk](./elastic-beanstalk.md)


---

# ⚔️ Service Comparison


|Service|Type|Best For|
|-|-|-|
|EC2|Virtual Server|Full control applications|
|Lambda|Serverless|Automation & events|
|Auto Scaling|Scaling Service|Production workloads|
|Elastic Beanstalk|PaaS|Fast deployments|


---

# 🔥 Common DevOps Architectures


## Highly Available Application


```text
Users

 ↓

Load Balancer

 ↓

Auto Scaling Group

 ↓

EC2 Instances

 ↓

Database
```

---

## Serverless Automation


```text
CloudWatch Event

        ↓

      Lambda

        ↓

 AWS Service Automation
```

Example:

```text
Stop unused EC2 instances automatically
```

---

## Managed Deployment


```text
Developer

↓

Git Repository

↓

Elastic Beanstalk

↓

Application Running
```

---

# 🛠️ Tools Used With Compute


## CI/CD

- Jenkins
- GitHub Actions


## Containers

- Docker
- Kubernetes


## Infrastructure Automation

- Terraform
- CloudFormation


## Monitoring

- CloudWatch
- CloudTrail


---

# 🔐 Compute Security Best Practices


✔ Never store AWS keys inside servers

✔ Use IAM Roles

✔ Allow only required ports

✔ Restrict SSH access

✔ Enable monitoring

✔ Update operating systems

✔ Use private subnets

✔ Take backups


---

# 📊 Monitoring Strategy


Monitor:

```text
Application

     ↓

CloudWatch Metrics

     ↓

CloudWatch Alarm

     ↓

SNS Alert
```


Important Metrics:

- CPU Usage
- Memory Usage
- Network
- Errors
- Logs

---

# 🎯 Interview Questions


## EC2

- What is EC2?
- Difference between AMI and Instance?
- Security Group vs NACL?
- How SSH works?


## Lambda

- What is serverless?
- Lambda timeout limit?
- Lambda triggers?
- IAM role usage?


## Auto Scaling

- What is desired capacity?
- Scaling policy types?
- How health checks work?


## Elastic Beanstalk

- Difference between EC2 and Beanstalk?
- Deployment strategies?

---

# 📂 Section Structure


```text
01-Compute/

├── README.md

├── ec2.md

├── lambda.md

├── auto-scaling.md

├── elastic-beanstalk.md

└── projects.md
```

---

# 🚀 Skills Gained


After completing this section:

✔ AWS Compute Fundamentals  
✔ Linux Server Deployment  
✔ Serverless Automation  
✔ Scaling Applications  
✔ Cloud Monitoring  
✔ Production Architecture Understanding  


---

## Status

AWS Compute Foundation Completed 🚀

Next:

💾 AWS Storage & Content Delivery
