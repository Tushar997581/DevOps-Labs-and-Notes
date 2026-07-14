# 🌎 Amazon CloudFront

# Complete Amazon CloudFront Guide for DevOps Engineers

Amazon CloudFront is AWS's Content Delivery Network (CDN) service that securely delivers websites, APIs, videos, and application content to users with low latency and high transfer speeds.

Instead of serving content from a single AWS Region, CloudFront caches content at AWS Edge Locations around the world, reducing the distance between users and the content they request.

CloudFront integrates with services like Amazon S3, Elastic Load Balancing (ELB), EC2, API Gateway, AWS WAF, and AWS Shield to improve application performance and security.

---

# 📖 What is a CDN?

Imagine your application is hosted in Mumbai.

Users:

- India ✅
- Japan
- Germany
- USA
- Australia

Without a CDN:

```text
USA User

      │

      ▼

Mumbai AWS Region

      │

Website Response
```

The request must travel thousands of kilometers.

Result:

❌ High latency

❌ Slow loading

❌ Poor user experience

---

With CloudFront:

```text
USA User

      │

      ▼

Nearest Edge Location

      │

Cached Content

      │

Instant Response
```

CloudFront serves content from the nearest Edge Location.

Result:

✔ Faster websites

✔ Lower latency

✔ Better performance

---

# Why Amazon CloudFront?

Modern applications serve:

- Images
- CSS
- JavaScript
- Videos
- APIs
- Downloads

If every request reaches the origin server:

```text
Users

↓

EC2

↓

High CPU

↓

More Network Traffic
```

CloudFront caches frequently requested content.

Benefits:

✔ Reduced server load

✔ Faster delivery

✔ Lower bandwidth cost

✔ Better scalability

---

# Amazon CloudFront Architecture

```text
                    Users

        ┌─────────┼──────────┐

        │         │          │

     India      Europe      USA

        │         │          │

        ▼         ▼          ▼

   Edge Location Edge Location Edge Location

              │

              ▼

        Amazon CloudFront

              │

      -----------------

      │               │

Amazon S3       Application Load Balancer

                      │

                 EC2 Instances
```

---

# Core Components

## Distribution

A Distribution is the primary CloudFront resource.

It defines:

- Origin
- Cache behavior
- SSL settings
- Security
- Performance

Types:

- Web Distribution
- RTMP (legacy)

---

## Origin

The origin is where CloudFront fetches content.

Supported origins:

✔ Amazon S3

✔ Application Load Balancer

✔ EC2

✔ API Gateway

✔ Custom HTTP Server

Example:

```text
CloudFront

↓

Origin

↓

S3 Bucket
```

---

## Edge Locations

Edge Locations are AWS data centers located worldwide.

Purpose:

Store cached copies closer to users.

Example:

```text
Mumbai

Delhi

Singapore

London

Frankfurt

Tokyo

New York
```

---

## Cache

CloudFront stores copies of frequently requested files.

Instead of requesting every file from the origin:

```text
User

↓

Edge Cache

↓

Response
```

This reduces latency.

---

## Cache Hit

Content exists in cache.

```text
User

↓

Edge Cache

↓

Response
```

Fastest response.

---

## Cache Miss

Content is unavailable in cache.

```text
User

↓

Edge Location

↓

Origin Server

↓

Cache Updated

↓

Response
```

Future requests become faster.

---

# Cache Behavior

Cache Behavior controls:

- Path patterns
- Allowed HTTP methods
- Compression
- TTL values
- Viewer protocol policy

Example:

```text
/images/*

↓

Cache

-----------------

/api/*

↓

Forward to Origin
```

---

# Time To Live (TTL)

TTL defines how long CloudFront stores cached content.

Example:

```text
Image

↓

Cached

↓

24 Hours

↓

Refresh
```

TTL values:

- Minimum TTL
- Default TTL
- Maximum TTL

---

# Cache Invalidation

Sometimes content changes before TTL expires.

Example:

```text
logo.png

↓

Updated

↓

Users still see old version
```

Solution:

Invalidate cache.

Example:

```text
/images/logo.png
```

CloudFront fetches the latest version.

---

# HTTPS & SSL

CloudFront supports HTTPS using:

- AWS Certificate Manager (ACM)
- Custom SSL Certificates

Benefits:

✔ Secure communication

✔ Data encryption

✔ Improved SEO

---

# Origin Access Control (OAC)

Recommended by AWS.

OAC allows CloudFront to securely access private S3 buckets.

Architecture:

```text
User

↓

CloudFront

↓

Origin Access Control

↓

Private S3 Bucket
```

Users cannot access the bucket directly.

---

# AWS WAF Integration

CloudFront integrates with AWS WAF.

Protection against:

- SQL Injection

- Cross Site Scripting

- Malicious Bots

- IP Blocking

Architecture:

```text
User

↓

AWS WAF

↓

CloudFront

↓

Application
```

---

# AWS Shield Integration

CloudFront automatically integrates with AWS Shield Standard.

Protects against:

✔ DDoS attacks

✔ Layer 3 attacks

✔ Layer 4 attacks

---

# Monitoring

Amazon CloudWatch provides metrics:

- Requests
- Cache Hit Rate
- Error Rate
- Bytes Downloaded
- Latency

CloudTrail records:

- API calls
- Configuration changes
- User activity

---

# AWS CLI

List distributions:

```bash
aws cloudfront list-distributions
```

Create invalidation:

```bash
aws cloudfront create-invalidation \
--distribution-id EXAMPLE123 \
--paths "/*"
```

Get distribution:

```bash
aws cloudfront get-distribution \
--id EXAMPLE123
```

---

# DevOps Use Cases

CloudFront is commonly used for:

✔ Static websites

✔ React applications

✔ Angular applications

✔ Next.js frontend

✔ API acceleration

✔ Video streaming

✔ Software downloads

✔ Global applications

---

# Best Practices

✔ Use Origin Access Control (OAC)

✔ Enable HTTPS

✔ Enable Compression

✔ Configure Cache Policies

✔ Use AWS WAF

✔ Enable Logging

✔ Monitor CloudWatch metrics

✔ Use custom domain names

---

# Troubleshooting

## Website Loading Slowly

Check:

- Cache hit ratio
- Origin performance
- TTL values

---

## Access Denied

Check:

- Bucket Policy
- Origin Access Control
- IAM permissions

---

## Old Content Displayed

Create Cache Invalidation.

---

## SSL Certificate Error

Verify:

- ACM certificate
- Alternate domain names
- DNS configuration

---

# Amazon CloudFront vs Amazon S3

| Feature | Amazon CloudFront | Amazon S3 |
|----------|-------------------|-----------|
| Service | CDN | Object Storage |
| Stores Files | No | Yes |
| Caches Content | Yes | No |
| Global Delivery | Yes | Limited |
| Performance | High | Standard |

---

# Interview Questions

### What is Amazon CloudFront?

Amazon CloudFront is AWS's Content Delivery Network (CDN) that delivers content using global Edge Locations.

---

### What is an Edge Location?

An AWS location that caches content closer to end users.

---

### Difference between Cache Hit and Cache Miss?

Cache Hit:

Content is available in the Edge Location.

Cache Miss:

CloudFront retrieves content from the Origin.

---

### What is an Origin?

The backend resource from which CloudFront fetches content.

Examples:

- Amazon S3
- EC2
- ALB
- API Gateway

---

### What is Cache Invalidation?

Removing cached objects before TTL expires so users receive updated content.

---

# Screenshot

```text
screenshots/

└── cloudfront/

    ├── cloudfront-overview.png

    └── cloudfront-hands-on-lab.png
```

---

# Official AWS References

- Amazon CloudFront Developer Guide
- AWS Well-Architected Framework
- AWS WAF Documentation
- AWS Shield Documentation
- AWS CLI Reference

---

# Skills Covered

✔ Content Delivery Networks (CDN)

✔ Edge Locations

✔ Cache Management

✔ HTTPS

✔ Origin Access Control

✔ AWS WAF Integration

✔ Cloud Monitoring

✔ Production Website Acceleration

---

# Status

Amazon CloudFront Completed 🌎🚀
