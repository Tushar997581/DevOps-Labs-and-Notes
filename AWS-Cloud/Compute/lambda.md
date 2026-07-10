# ⚡ AWS Lambda for DevOps Engineers

## Complete Serverless Compute Guide

AWS Lambda is a serverless compute service that allows you to run code without provisioning or managing servers.

Lambda automatically handles:

- Server provisioning
- Scaling
- Availability
- Infrastructure management

Developers only focus on writing code.

---

# 📌 What is AWS Lambda?

Traditional Server:

```text
Developer

   ↓

Manage EC2 Server

   ↓

Install Runtime

   ↓

Deploy Application

   ↓

Manage Scaling
```

Lambda:

```text
Developer

   ↓

Upload Code

   ↓

AWS Lambda Executes

   ↓

Auto Scaling
```

Lambda follows:

```text
Function as a Service (FaaS)
```

---

# 🚀 Why DevOps Engineers Use Lambda?

Lambda is used for:

- Automation tasks
- Event processing
- Scheduled jobs
- Serverless applications
- File processing
- Monitoring automation
- Infrastructure operations


Examples:

✔ Automatically backup resources  
✔ Resize uploaded images  
✔ Process S3 files  
✔ Send alerts  
✔ Automate AWS operations  

---

# 🏗️ Lambda Architecture


```text
        Event Source

             |

             ↓

        AWS Lambda

             |

             ↓

        Execution Role

             |

             ↓

       AWS Services


Examples:

S3 → Lambda → SNS

CloudWatch → Lambda → EC2

API Gateway → Lambda → Database
```

---

# 🔥 Lambda Core Components


# 1. Lambda Function


A function contains your application code.


Example:

Python:

```python
def lambda_handler(event, context):

    return "Hello AWS Lambda"
```

---

# 2. Runtime


Runtime provides the programming environment.


Supported examples:

- Python
- Node.js
- Java
- Go
- .NET


Example:

```text
Python 3.x Runtime

        ↓

Execute Python Function
```

---

# 3. Handler


Handler is the entry point of Lambda execution.


Example:

```python
def lambda_handler(event, context):
```


AWS calls this method when function runs.

---

# 4. Event


Events trigger Lambda execution.


Examples:

```text
S3 Upload

API Request

CloudWatch Schedule

SNS Message
```

---

# 5. Execution Role (IAM Role)


Lambda needs permissions using IAM roles.


Example:


Lambda needs access to S3:


```text
Lambda Function

        ↓

IAM Role

        ↓

Amazon S3
```


Never store AWS keys inside Lambda code.

---

# 6. Timeout


Maximum time Lambda can run.


Default:

```text
3 seconds
```


Maximum:

```text
15 minutes
```


Useful to prevent stuck functions.

---

# 7. Memory Configuration


Memory affects:

- RAM
- CPU power


Range:

```text
128 MB → 10 GB+
```

---

# ⚙️ Lambda Invocation Types


# 1. Synchronous Invocation


Request waits for response.


Example:

```text
API Gateway

↓

Lambda

↓

Response
```


Used for:

- APIs
- Web applications


---

# 2. Asynchronous Invocation


Event sent and Lambda runs later.


Example:

```text
S3 Upload

↓

Lambda Processing
```


Used for:

- Background tasks
- Automation

---

# 3. Event Source Mapping


Lambda polls services.


Examples:

- SQS
- DynamoDB Streams

---

# 🔥 Common Lambda Triggers


# S3 Trigger


Example:


```text
Upload File

↓

S3 Bucket

↓

Lambda Function
```


Use cases:

- Image processing
- Log processing
- File validation


---

# CloudWatch EventBridge Trigger


Run Lambda on schedule.


Example:


```text
Every Night 12 AM

↓

Lambda Backup Script
```


Cron example:

```text
cron(0 0 * * ? *)
```

---

# SNS Trigger


Architecture:

```text
SNS Topic

↓

Lambda

↓

Process Message
```

---

# API Gateway Trigger


Create serverless APIs.


```text
User

↓

API Gateway

↓

Lambda

↓

Database
```

---

# 📊 Lambda Monitoring


Using CloudWatch:


Monitor:

- Invocations
- Errors
- Duration
- Logs
- Throttles


View logs:

```text
CloudWatch

↓

Log Groups

↓

Lambda Logs
```

---

# 🧪 Practical Lab 1

## Create First Lambda Function


Steps:


1. Open Lambda Console

2. Create Function

3. Choose:

```text
Author from scratch
```

4. Runtime:

```text
Python
```

5. Create Execution Role

6. Deploy Function

---

# Example Function


```python
import json


def lambda_handler(event, context):

    return {

        "statusCode":200,

        "body":"Hello DevOps Engineer"

    }
```

---

# 🧪 Practical Lab 2

## EC2 Start Stop Automation


Architecture:


```text
EventBridge Schedule

        ↓

Lambda

        ↓

EC2 API
```


IAM permission:

```text
ec2:StartInstances

ec2:StopInstances
```


Python example:

```python
import boto3


ec2=boto3.client('ec2')


def lambda_handler(event,context):

    ec2.stop_instances(
    
    InstanceIds=['instance-id']
    
    )
```

---

# 🧪 Practical Lab 3

## S3 Upload Notification


Architecture:


```text
File Upload

↓

S3

↓

Lambda

↓

SNS Email Alert
```


Real use:

- Backup notification
- Security alerts

---

# AWS CLI Commands


List functions:

```bash
aws lambda list-functions
```


Invoke function:

```bash
aws lambda invoke \
--function-name my-function \
output.json
```


Delete:

```bash
aws lambda delete-function \
--function-name my-function
```

---

# 🔐 Lambda Security Best Practices


✔ Use IAM roles

✔ Least privilege permissions

✔ Enable CloudWatch logs

✔ Use environment variables

✔ Store secrets in Secrets Manager

✔ Avoid hardcoded credentials

✔ Monitor errors

---

# 🔥 Troubleshooting


## Lambda Timeout


Check:

- Timeout settings
- Code performance
- Network calls


Increase timeout if required.

---

# Permission Error


Example:

```text
AccessDeniedException
```


Fix:

Check IAM Role permissions.

---

# Function Not Triggering


Check:

- Trigger configuration
- IAM permissions
- CloudWatch logs

---

# Lambda vs EC2


| EC2 | Lambda |
|-|-|
|Virtual Server|Serverless|
|Manual Scaling|Auto Scaling|
|Pay Running Time|Pay Execution Time|
|Manage OS|No OS Management|
|Long Running Apps|Short Tasks|

---

# 🎯 DevOps Use Cases


Lambda is used for:

✔ AWS automation  
✔ Backup workflows  
✔ Monitoring alerts  
✔ Serverless APIs  
✔ Scheduled operations  
✔ Event processing  

---

# 🚀 Skills Covered


- Serverless Computing
- AWS Automation
- IAM Integration
- Event Driven Architecture
- CloudWatch Monitoring
- Infrastructure Automation
