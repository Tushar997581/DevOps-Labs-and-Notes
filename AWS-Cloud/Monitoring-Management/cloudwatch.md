# 📊 Amazon CloudWatch

# Complete Amazon CloudWatch Guide for DevOps Engineers

Amazon CloudWatch is a fully managed monitoring and observability service that helps you monitor AWS resources, applications, infrastructure, and services in real time.

CloudWatch collects metrics, logs, and events from AWS resources and allows you to visualize data using dashboards, create alarms, automate actions, and troubleshoot applications.

It enables DevOps teams to proactively monitor application health, infrastructure performance, and operational issues.

---

# 📖 What is Amazon CloudWatch?

Imagine a hospital.

Doctors constantly monitor patients using machines that display:

- Heart Rate
- Blood Pressure
- Oxygen Level
- Temperature

If something abnormal happens, an alarm immediately alerts the medical staff.

CloudWatch works in the same way.

```text
AWS Resources

↓

CloudWatch

↓

Metrics & Logs

↓

Alarms

↓

Notifications
```

Instead of monitoring people, CloudWatch monitors your cloud infrastructure.

---

# Why Do We Need CloudWatch?

Without monitoring:

```text
EC2

↓

CPU = 100%

↓

Nobody Knows

↓

Application Crash
```

With CloudWatch:

```text
EC2

↓

CloudWatch

↓

Alarm

↓

Amazon SNS

↓

DevOps Engineer
```

Benefits:

✔ Real-Time Monitoring

✔ Infrastructure Visibility

✔ Automatic Alerts

✔ Performance Analysis

✔ Faster Troubleshooting

✔ Automation

---

# CloudWatch Architecture

```text
                 AWS Resources

 EC2      RDS      Lambda      ALB      EBS

   │         │         │         │        │

   └─────────┼─────────┼─────────┼────────┘

                    ▼

             Amazon CloudWatch

      ┌──────────┬──────────┬──────────┐

      │          │          │

   Metrics      Logs     Events

      │          │          │

      └──────────┼──────────┘

                 ▼

             Dashboards

                 │

              Alarms

                 │

             Amazon SNS

                 │

         Email / SMS / Lambda
```

---

# Core Components

Amazon CloudWatch consists of:

- Metrics
- Namespaces
- Dimensions
- Logs
- Log Groups
- Log Streams
- Dashboards
- Alarms
- Events
- CloudWatch Agent
- Log Insights
- Contributor Insights
- Composite Alarms

---

# Metrics

Metrics are numerical measurements collected over time.

Examples:

- CPU Utilization
- Memory Usage
- Network In
- Network Out
- Disk Read Operations
- Disk Write Operations

Example:

```text
CPU Utilization

10%

20%

35%

80%

95%
```

CloudWatch stores metric history for analysis and visualization.

---

# Namespaces

A Namespace groups related metrics.

Examples:

```text
AWS/EC2

AWS/RDS

AWS/S3

AWS/Lambda

Custom/MyApplication
```

Namespaces help organize metrics by service or application.

---

# Dimensions

Dimensions add context to metrics.

Example:

```text
Metric

CPUUtilization

↓

Dimension

InstanceId = i-123456789
```

Common dimensions:

- InstanceId
- AutoScalingGroupName
- LoadBalancer
- FunctionName

---

# CloudWatch Logs

CloudWatch Logs store application and system logs.

Examples:

- Application Logs
- Nginx Logs
- Apache Logs
- System Logs
- Lambda Logs
- VPC Flow Logs

Logs help troubleshoot issues and analyze application behavior.

---

# Log Groups

A Log Group is a collection of related log streams.

Example:

```text
Application Logs

↓

Log Group

↓

/aws/ec2/webserver
```

---

# Log Streams

A Log Stream contains logs from a single source.

Example:

```text
Log Group

↓

EC2-WebServer

↓

Log Stream

↓

Today's Logs
```

---

# CloudWatch Agent

The CloudWatch Agent collects additional operating system metrics from EC2 instances.

Examples:

- Memory Usage
- Disk Usage
- Swap Usage
- Processes
- File System Metrics

Install on Amazon Linux:

```bash
sudo yum install amazon-cloudwatch-agent
```

Start the agent:

```bash
sudo systemctl start amazon-cloudwatch-agent
```

---

# Dashboards

Dashboards provide a centralized view of AWS metrics.

Example Dashboard:

```text
CPU

Memory

Disk

Network

Requests

Errors
```

Dashboards support multiple widgets and multiple AWS services.

---

# Alarms

CloudWatch Alarms monitor metrics and perform actions when thresholds are reached.

Example:

```text
CPU > 80%

↓

Alarm

↓

Send Email
```

Alarm States:

- OK
- ALARM
- INSUFFICIENT_DATA

---

# Composite Alarms

Composite Alarms combine multiple alarms into one.

Example:

```text
CPU Alarm

+

Memory Alarm

↓

Composite Alarm

↓

Notify DevOps
```

This reduces unnecessary alerts.

---

# Events (Amazon EventBridge)

CloudWatch Events are now part of Amazon EventBridge.

Example:

```text
EC2 Stops

↓

EventBridge

↓

Lambda

↓

Restart EC2
```

Useful for automation and event-driven architectures.

---

# CloudWatch Log Insights

CloudWatch Logs Insights enables interactive querying of log data.

Example:

```sql
fields @timestamp, @message
| sort @timestamp desc
| limit 20
```

Useful for:

- Troubleshooting
- Log Analysis
- Error Investigation

---

# Contributor Insights

Contributor Insights identifies the most frequent contributors to system performance.

Example:

```text
Top IP Addresses

Top API Calls

Top Error Sources
```

---

# Custom Metrics

Applications can publish their own metrics.

Example:

```text
Orders Processed

Payments Completed

Active Users
```

Publish using AWS CLI:

```bash
aws cloudwatch put-metric-data \
--namespace MyApplication \
--metric-name OrdersProcessed \
--value 250
```

---

# AWS CLI

View metrics:

```bash
aws cloudwatch list-metrics
```

Describe alarms:

```bash
aws cloudwatch describe-alarms
```

Get metric statistics:

```bash
aws cloudwatch get-metric-statistics
```

---

# AWS Console Navigation

```text
AWS Console

↓

CloudWatch

↓

Metrics

↓

Dashboards

↓

Alarms

↓

Logs
```

---

# DevOps Use Cases

CloudWatch is commonly used for:

✔ EC2 Monitoring

✔ Lambda Monitoring

✔ RDS Monitoring

✔ Auto Scaling

✔ Kubernetes Monitoring

✔ Container Monitoring

✔ Infrastructure Dashboards

✔ Log Analysis

✔ Alerting

✔ Capacity Planning

---

# Best Practices

✔ Create meaningful dashboards

✔ Configure alarms for critical metrics

✔ Monitor trends instead of isolated values

✔ Use CloudWatch Agent for memory and disk metrics

✔ Enable log retention policies

✔ Use custom metrics for business KPIs

✔ Integrate alarms with Amazon SNS

✔ Regularly review alarm thresholds

---

# Monitoring Metrics

Typical production metrics include:

- CPU Utilization
- Memory Utilization
- Disk Utilization
- Network Traffic
- Request Count
- Latency
- Error Rate
- Healthy Host Count
- Database Connections

---

# Troubleshooting

## High CPU

Check:

- Running processes
- Auto Scaling
- Application load

---

## Alarm Not Triggered

Verify:

- Correct metric
- Correct threshold
- Evaluation period
- SNS configuration

---

## Missing Logs

Check:

- CloudWatch Agent
- IAM Role
- Log Group
- Agent status

---

# 🏢 Real Production Scenario

## Production Web Application Monitoring

```text
                      Users

                        │

             Application Load Balancer

                        │

              Auto Scaling Group

          ┌─────────────┼─────────────┐

          │             │             │

        EC2-A         EC2-B        EC2-C

             │            │            │

             └────────────┼────────────┘

                          │

                     Amazon RDS

                          │

                    CloudWatch

      ┌─────────────┼─────────────┐

      │             │             │

   Metrics        Logs         Alarms

                          │

                     Amazon SNS

                          │

                 Email Notification

                          │

                   DevOps Engineer
```

### Workflow

1. CloudWatch collects metrics from EC2, ALB, and RDS.
2. Dashboards display infrastructure health.
3. Alarms monitor thresholds such as CPU > 80%.
4. SNS sends notifications when alarms trigger.
5. Engineers investigate logs using CloudWatch Logs Insights.
6. Auto Scaling launches new instances if required.

Benefits:

✔ Proactive Monitoring

✔ Reduced Downtime

✔ Faster Incident Response

✔ Improved Availability

---

# CloudWatch vs CloudTrail

| Feature | CloudWatch | CloudTrail |
|----------|------------|------------|
| Purpose | Monitoring | Auditing |
| Data | Metrics & Logs | API Calls |
| Alarms | Yes | No |
| Dashboards | Yes | No |
| Security Auditing | Limited | Yes |

---

# Interview Questions

### What is Amazon CloudWatch?

Amazon CloudWatch is a monitoring and observability service for AWS resources and applications.

---

### What are CloudWatch Metrics?

Numerical measurements collected over time from AWS resources.

---

### What is a CloudWatch Alarm?

A monitoring rule that performs actions when a metric reaches a specified threshold.

---

### What is the difference between Log Groups and Log Streams?

A Log Group contains related Log Streams.

A Log Stream contains log events from a single source.

---

### Can CloudWatch monitor memory usage?

Yes, by installing and configuring the CloudWatch Agent on EC2 instances.

---

# Screenshot

```text
screenshots/

└── cloudwatch/

    ├── 01-dashboard.png
    ├── 02-metrics.png
    ├── 03-log-group.png
    ├── 04-alarm.png
    ├── 05-cloudwatch-agent.png
    ├── 06-log-insights.png
    ├── 07-dashboard-widget.png
    └── cloudwatch-complete-lab.png
```

---

# Official AWS References

- Amazon CloudWatch User Guide
- CloudWatch Logs User Guide
- Amazon EventBridge User Guide
- AWS CLI Command Reference
- AWS Well-Architected Framework

---

# Quick Revision

```text
CloudWatch → Monitoring

Metrics → Performance Data

Logs → Application & System Logs

Dashboards → Visualization

Alarms → Notifications

Agent → Memory & Disk Metrics

Log Insights → Query Logs

SNS → Alert Notifications
```

---

# Skills Covered

✔ CloudWatch Metrics

✔ CloudWatch Logs

✔ Dashboards

✔ Alarms

✔ CloudWatch Agent

✔ Log Insights

✔ EventBridge Integration

✔ Infrastructure Monitoring

✔ Production Monitoring

---

# Status

Amazon CloudWatch Completed 📊🚀
