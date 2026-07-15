# 🛡️ AWS Web Application Firewall (AWS WAF)

# Complete AWS WAF Guide for DevOps Engineers

AWS Web Application Firewall (AWS WAF) is a managed security service that protects web applications from common web exploits and malicious traffic.

AWS WAF filters and monitors HTTP and HTTPS requests before they reach your application. It allows you to define security rules that permit, block, or monitor incoming requests.

AWS WAF integrates with:

- Application Load Balancer (ALB)
- Amazon CloudFront
- Amazon API Gateway
- AWS App Runner
- Amazon Cognito

---

# 📖 What is AWS WAF?

Imagine a shopping mall.

Every visitor enters through a security checkpoint.

The security team checks:

- Identity
- Suspicious items
- Dangerous objects

Only safe visitors are allowed inside.

AWS WAF works similarly.

```text
Internet

↓

AWS WAF

↓

Application Load Balancer

↓

EC2 Application
```

Before requests reach your application, WAF evaluates them against security rules.

---

# Why Do We Need AWS WAF?

Without WAF:

```text
Internet

↓

Application

↓

SQL Injection

↓

Database
```

Problems:

❌ SQL Injection

❌ Cross-Site Scripting (XSS)

❌ Bot attacks

❌ Credential stuffing

❌ Layer 7 DDoS attacks

---

With WAF:

```text
Internet

↓

AWS WAF

↓

Allow

↓

Application
```

Malicious traffic is blocked before reaching your application.

Benefits:

✔ Improved security

✔ Reduced attack surface

✔ Layer 7 protection

✔ Managed security rules

---

# AWS WAF Architecture

```text
                  Internet

                      │

               AWS WAF (Web ACL)

                      │

         Application Load Balancer

                      │

                 EC2 Instances

                      │

                 Amazon RDS
```

---

# Components of AWS WAF

```text
AWS WAF

│

├── Web ACL

├── Rules

├── Rule Groups

├── Managed Rule Groups

├── Custom Rules

└── Rate-Based Rules
```

---

# Web ACL

A Web ACL is a collection of security rules.

Example:

```text
Web ACL

↓

SQL Injection Rule

↓

XSS Rule

↓

IP Block Rule

↓

Allow Traffic
```

Every protected resource must be associated with a Web ACL.

---

# Rules

Rules define how requests are evaluated.

Possible actions:

- Allow
- Block
- Count
- CAPTCHA
- Challenge

Example:

```text
IF

Country = Unknown

↓

Block
```

---

# Managed Rule Groups

AWS provides managed security rules.

Examples:

- Core Rule Set
- SQL Injection Protection
- Linux Protection
- PHP Protection
- WordPress Protection

Benefits:

✔ Automatically updated

✔ Easy to configure

✔ Recommended for production

---

# Custom Rules

You can create your own rules.

Example:

```text
URI = /admin

AND

IP ≠ Company Office

↓

Block
```

Useful for organization-specific security requirements.

---

# Rate-Based Rules

Rate-based rules protect against excessive requests.

Example:

```text
IP Address

↓

More than 1000 requests

↓

5 Minutes

↓

Block
```

Helps reduce bot traffic and abuse.

---

# IP Set

An IP Set contains trusted or blocked IP addresses.

Example:

```text
Allowed

203.0.113.10

203.0.113.11
```

Blocked:

```text
198.51.100.25
```

---

# Geographic Restrictions

AWS WAF can allow or block requests based on country.

Example:

```text
India

↓

Allow

------------

Unknown Region

↓

Block
```

Useful when applications are intended for specific regions.

---

# Bot Protection

AWS WAF can detect and manage bot traffic.

Examples:

- Web crawlers
- Scrapers
- Credential stuffing bots
- Automated login attempts

---

# CAPTCHA & Challenge

AWS WAF supports CAPTCHA and Challenge actions.

Example:

```text
Suspicious User

↓

CAPTCHA

↓

Human Verified

↓

Application
```

This helps distinguish legitimate users from automated bots.

---

# AWS CLI

Create Web ACL:

```bash
aws wafv2 create-web-acl
```

List Web ACLs:

```bash
aws wafv2 list-web-acls
```

Associate Web ACL:

```bash
aws wafv2 associate-web-acl
```

---

# AWS Console Navigation

```text
AWS Console

↓

AWS WAF & Shield

↓

Web ACLs

↓

Create Web ACL

↓

Associate Resource
```

---

# DevOps Use Cases

AWS WAF is commonly used for:

✔ Public Web Applications

✔ APIs

✔ E-Commerce Platforms

✔ Banking Applications

✔ SaaS Platforms

✔ CloudFront Distributions

✔ Application Load Balancers

---

# Best Practices

✔ Use AWS Managed Rule Groups

✔ Enable logging

✔ Monitor blocked requests

✔ Use rate limiting

✔ Protect login pages

✔ Block suspicious IPs

✔ Review Web ACL rules regularly

✔ Combine with AWS Shield

---

# Monitoring

AWS WAF integrates with:

- Amazon CloudWatch
- AWS CloudTrail
- Amazon Kinesis Data Firehose

Metrics include:

- Allowed Requests
- Blocked Requests
- Counted Requests
- CAPTCHA Requests

---

# Troubleshooting

## Legitimate Users Blocked

Check:

- Web ACL rules
- IP sets
- Rate limits

---

## SQL Injection Not Blocked

Verify:

- Managed Rule Group enabled
- Rule priority
- Rule action

---

## High False Positives

Review:

- Custom rules
- Managed rules
- Logs

---

# 🏢 Real Production Scenario

## Secure E-Commerce Website

```text
                    Users

                      │

                  Route 53

                      │

                CloudFront CDN

                      │

                  AWS WAF

                      │

          Application Load Balancer

                      │

          Auto Scaling Group (EC2)

                      │

                 Amazon RDS
```

### Request Flow

1. Users access the website.
2. Route 53 resolves the domain.
3. CloudFront serves cached content when available.
4. AWS WAF inspects every HTTP/HTTPS request.
5. Malicious requests are blocked.
6. Valid requests reach the Application Load Balancer.
7. Traffic is distributed across healthy EC2 instances.
8. Application data is stored in Amazon RDS.

Benefits:

✔ SQL Injection Protection

✔ XSS Protection

✔ Bot Protection

✔ Rate Limiting

✔ Secure Public Applications

---

# AWS WAF vs Security Groups

| Feature | AWS WAF | Security Group |
|----------|----------|----------------|
| Layer | Layer 7 | Layer 4 |
| Traffic | HTTP/HTTPS | Network |
| SQL Injection Protection | Yes | No |
| XSS Protection | Yes | No |
| IP Blocking | Yes | Yes |
| Geographic Blocking | Yes | No |

---

# Interview Questions

### What is AWS WAF?

AWS WAF is a managed web application firewall that protects web applications from common web exploits.

---

### What is a Web ACL?

A Web ACL is a collection of rules that inspect HTTP and HTTPS requests.

---

### Can AWS WAF protect EC2 directly?

No.

AWS WAF protects supported services such as Application Load Balancers, CloudFront, API Gateway, App Runner, and Amazon Cognito.

---

### What attacks does AWS WAF help prevent?

- SQL Injection
- Cross-Site Scripting (XSS)
- Bot attacks
- Credential stuffing
- Layer 7 DDoS attacks

---

# Screenshot

```text
screenshots/

└── waf/

    ├── web-acl.png
    ├── managed-rules.png
    ├── rate-limit-rule.png
    ├── associate-resource.png
    └── waf-complete-lab.png
```

---

# Official AWS References

- AWS WAF Developer Guide
- AWS Security Best Practices
- AWS Well-Architected Framework
- AWS CLI Command Reference

---

# Quick Revision

```text
AWS WAF → Web Application Firewall

Protects → HTTP/HTTPS Applications

Web ACL → Collection of Rules

Managed Rules → AWS Maintained

Custom Rules → User Defined

Rate Limiting → Blocks Excessive Requests

Best Used With → CloudFront & ALB
```

---

# Skills Covered

✔ AWS WAF

✔ Web ACL

✔ Managed Rules

✔ Custom Rules

✔ Rate Limiting

✔ SQL Injection Protection

✔ XSS Protection

✔ Production Web Security

---

# Status

AWS WAF Completed 🛡️🚀
