# 📨 Amazon Simple Notification Service (Amazon SNS)

# Complete Amazon SNS Guide for DevOps Engineers

Amazon Simple Notification Service (Amazon SNS) is a fully managed messaging and notification service that enables applications, AWS services, and users to communicate through notifications and event-driven messaging.

SNS follows a **publish/subscribe (Pub/Sub)** messaging model where publishers send messages to a topic, and subscribers automatically receive those messages.

Amazon SNS supports multiple endpoints including:

- Email
- SMS
- HTTP/HTTPS
- AWS Lambda
- Amazon SQS
- Mobile Push Notifications

SNS helps build scalable, loosely coupled, and event-driven applications.

---

# 📖 What is Amazon SNS?

Imagine a school principal wants to announce an important message.

Instead of calling every student individually, the principal makes one announcement.

```text
Principal

↓

Speaker

↓

All Students
```

Amazon SNS works the same way.

```text
Publisher

↓

SNS Topic

↓

Subscribers
```

One published message can reach multiple subscribers simultaneously.

---

# Why Do We Need SNS?

Without SNS:

```text
CloudWatch Alarm

↓

Developer A

↓

Developer B

↓

Developer C
```

Each notification must be sent individually.

Problems:

❌ Complex application logic

❌ Slow notifications

❌ Difficult scalability

With SNS:

```text
CloudWatch Alarm

↓

SNS Topic

↓

Email

SMS

Lambda

SQS
```

Benefits:

✔ Instant Notifications

✔ Event-Driven Architecture

✔ High Scalability

✔ Multiple Subscribers

✔ Fully Managed

---

# Amazon SNS Architecture

```text
                Publisher

                    │

                    ▼

               Amazon SNS

                    │

        ┌───────────┼───────────┐

        │           │           │

      Email       Lambda       SQS

        │

      DevOps Team
```

---

# Publish/Subscribe Model

Amazon SNS uses the Publish/Subscribe pattern.

```text
Publisher

↓

SNS Topic

↓

Subscribers
```

Publisher:

Sends messages.

Subscribers:

Receive messages automatically.

---

# Components of SNS

```text
Amazon SNS

│

├── Topics

├── Publishers

├── Subscribers

├── Subscriptions

└── Messages
```

---

# SNS Topics

A Topic is a communication channel.

Example:

```text
Production Alerts

↓

Topic
```

Every message is published to a Topic.

Example Topics:

- EC2 Alerts
- Billing Alerts
- Security Alerts
- Deployment Notifications

---

# Publishers

Publishers send messages.

Examples:

- CloudWatch
- Lambda
- EventBridge
- EC2
- Custom Applications

---

# Subscribers

Subscribers receive notifications.

Supported subscriber types:

- Email
- SMS
- HTTP Endpoint
- HTTPS Endpoint
- Lambda
- Amazon SQS
- Mobile Push

---

# Subscription

A Subscription connects a Topic to an endpoint.

```text
Topic

↓

Subscription

↓

Email
```

Confirmation is required for email subscriptions.

---

# Message Flow

```text
CloudWatch Alarm

↓

SNS Topic

↓

Email

↓

DevOps Engineer
```

---

# Supported Protocols

| Protocol | Supported |
|----------|-----------|
| Email | ✅ |
| SMS | ✅ |
| HTTP | ✅ |
| HTTPS | ✅ |
| Lambda | ✅ |
| Amazon SQS | ✅ |
| Mobile Push | ✅ |

---

# Fan-Out Architecture

SNS supports the Fan-Out messaging pattern.

```text
Application

↓

SNS Topic

↓

Lambda

↓

Email

↓

Amazon SQS

↓

Analytics System
```

One message reaches multiple systems simultaneously.

---

# SNS + CloudWatch

Most production environments use:

```text
CPU > 80%

↓

CloudWatch Alarm

↓

SNS

↓

Email Alert
```

---

# SNS + Lambda

```text
SNS

↓

Lambda

↓

Restart EC2

↓

Create Ticket

↓

Send Slack Notification
```

---

# SNS + Amazon SQS

```text
Application

↓

SNS

↓

Queue A

Queue B

Queue C
```

Useful for decoupled microservices.

---

# SNS + EventBridge

```text
AWS Event

↓

EventBridge

↓

SNS

↓

Email
```

---

# Message Filtering

Subscribers can receive only specific messages.

Example:

```text
Severity = Critical

↓

DevOps Team

------------

Severity = Warning

↓

Operations Team
```

---

# FIFO Support

SNS supports FIFO Topics.

Benefits:

✔ Ordered Delivery

✔ Exactly Once Processing

Useful for:

- Banking
- Financial Transactions
- Inventory Systems

---

# Security

SNS integrates with:

- IAM
- AWS KMS
- VPC Endpoints

Security Features:

✔ Encryption

✔ Access Policies

✔ IAM Authentication

✔ Secure Publishing

---

# AWS CLI

Create Topic:

```bash
aws sns create-topic \
--name production-alerts
```

List Topics:

```bash
aws sns list-topics
```

Subscribe Email:

```bash
aws sns subscribe \
--topic-arn TOPIC_ARN \
--protocol email \
--notification-endpoint your-email@example.com
```

Publish Message:

```bash
aws sns publish \
--topic-arn TOPIC_ARN \
--message "CPU Utilization exceeded 80%"
```

---

# AWS Console Navigation

```text
AWS Console

↓

Amazon SNS

↓

Topics

↓

Subscriptions

↓

Publish Message
```

---

# DevOps Use Cases

Amazon SNS is commonly used for:

✔ CloudWatch Alerts

✔ Deployment Notifications

✔ Auto Scaling Notifications

✔ Security Alerts

✔ Billing Alerts

✔ Lambda Triggers

✔ Disaster Recovery

✔ Incident Management

✔ Event-Driven Applications

---

# Best Practices

✔ Use descriptive Topic names

✔ Encrypt sensitive Topics

✔ Enable delivery status logging

✔ Use Message Filtering

✔ Restrict Topic access using IAM

✔ Remove unused subscriptions

✔ Monitor failed deliveries

✔ Use FIFO Topics when ordering matters

---

# Troubleshooting

## Email Not Received

Check:

- Subscription confirmation
- Spam folder
- Correct email address

---

## CloudWatch Alarm Not Sending Email

Verify:

- SNS Topic
- Alarm Action
- Subscription status

---

## Lambda Not Triggered

Check:

- SNS permissions
- Lambda permissions
- Subscription configuration

---

# 🏢 Real Production Scenario

## Infrastructure Monitoring & Notifications

```text
                    Amazon EC2

                        │

                  CloudWatch

                        │

                  CPU > 80%

                        │

                CloudWatch Alarm

                        │

                  Amazon SNS

        ┌───────────────┼───────────────┐

        │               │               │

     Email         Lambda        Amazon SQS

        │               │               │

 DevOps Team     Auto Recovery    Ticket System
```

### Workflow

1. CloudWatch detects high CPU utilization.
2. The CloudWatch Alarm changes to the ALARM state.
3. The alarm publishes a message to an SNS Topic.
4. SNS sends an email to the DevOps team.
5. SNS invokes a Lambda function for automated recovery.
6. SNS sends the same event to Amazon SQS for downstream processing.

Benefits:

✔ Instant Alerts

✔ Automatic Recovery

✔ Centralized Notifications

✔ Event-Driven Automation

---

# Amazon SNS vs Amazon SQS

| Feature | SNS | SQS |
|----------|-----|-----|
| Type | Pub/Sub | Message Queue |
| Push Messages | Yes | No |
| Multiple Subscribers | Yes | No |
| Message Storage | Temporary | Until Consumed |
| Best For | Notifications | Decoupling Applications |

---

# Interview Questions

### What is Amazon SNS?

Amazon SNS is a fully managed publish/subscribe messaging service used for notifications and event-driven communication.

---

### What is an SNS Topic?

A Topic is a communication channel where publishers send messages and subscribers receive them.

---

### Can one SNS Topic have multiple subscribers?

Yes.

One Topic can deliver the same message to multiple subscribers simultaneously.

---

### What is the difference between SNS and SQS?

SNS pushes messages to subscribers immediately.

SQS stores messages until consumers retrieve them.

---

### Which AWS services commonly integrate with SNS?

- CloudWatch
- Lambda
- EventBridge
- SQS
- Auto Scaling
- AWS Backup

---

# Screenshot

```text
screenshots/

└── sns/

    ├── 01-create-topic.png
    ├── 02-email-subscription.png
    ├── 03-confirm-subscription.png
    ├── 04-publish-message.png
    ├── 05-cloudwatch-alarm.png
    ├── 06-email-received.png
    └── sns-complete-lab.png
```

---

# Official AWS References

- Amazon SNS Developer Guide
- Amazon SNS API Reference
- AWS CLI Command Reference
- AWS Well-Architected Framework
- AWS Messaging Best Practices

---

# Quick Revision

```text
SNS → Notification Service

Topic → Communication Channel

Publisher → Sends Messages

Subscriber → Receives Messages

Pub/Sub → Publish & Subscribe Model

Supports → Email, SMS, Lambda, SQS, HTTP/HTTPS

Best For → Alerts & Event-Driven Applications
```

---

# Skills Covered

✔ Amazon SNS

✔ Topics

✔ Publishers

✔ Subscribers

✔ Message Filtering

✔ Fan-Out Architecture

✔ CloudWatch Integration

✔ Lambda Integration

✔ SQS Integration

✔ Production Notifications

---

# Status

Amazon SNS Completed 📨🚀
