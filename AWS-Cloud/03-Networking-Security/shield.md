# 🛡️ AWS Shield

# Complete AWS Shield Guide for DevOps Engineers

AWS Shield is a managed Distributed Denial of Service (DDoS) protection service that safeguards AWS applications from network and application layer attacks.

AWS Shield continuously monitors traffic entering AWS resources and automatically detects and mitigates DDoS attacks.

AWS Shield is integrated with services such as:

- Amazon CloudFront
- Route 53
- Elastic Load Balancing (ALB/NLB)
- AWS Global Accelerator

AWS Shield helps maintain application availability during attacks without requiring manual intervention.

---

# 📖 What is AWS Shield?

Imagine a shopping mall.

Normally:

```text
100 Customers

↓

Main Entrance

↓

Shopping Mall
```

During an attack:

```text
10 Million Fake Requests

↓

Main Entrance

↓

Mall Becomes Unusable
```

AWS Shield works like a professional security team.

```text
Internet

↓

AWS Shield

↓

Legitimate Requests

↓

Application
```

Malicious traffic is detected and filtered before it reaches your application.

---

# Why Do We Need AWS Shield?

Without AWS Shield:

```text
Internet

↓

Massive DDoS Attack

↓

Application Down
```

Problems:

❌ Website unavailable

❌ Revenue loss

❌ Poor customer experience

❌ Infrastructure overload

---

With AWS Shield:

```text
Internet

↓

AWS Shield

↓

Attack Mitigation

↓

Application
```

Benefits:

✔ Automatic DDoS protection

✔ Improved availability

✔ Low latency

✔ Integrated with AWS networking services

---

# AWS Shield Architecture

```text
                    Internet

                        │

                DDoS Attack

                        │

                   AWS Shield

                        │

                  AWS WAF (Optional)

                        │

                CloudFront CDN

                        │

          Application Load Balancer

                        │

             Auto Scaling Group

                        │

                 Amazon RDS
```

---

# Types of AWS Shield

AWS provides two editions.

```text
AWS Shield

│

├── Shield Standard

└── Shield Advanced
```

---

# Shield Standard

Shield Standard is automatically enabled for all AWS customers at no additional charge.

Features:

✔ Always enabled

✔ Automatic protection

✔ Protection against common Layer 3 and Layer 4 attacks

Protects services including:

- CloudFront
- Route 53
- Global Accelerator
- Elastic Load Balancing

---

# Shield Advanced

Shield Advanced provides additional protection for mission-critical applications.

Features:

✔ Advanced attack detection

✔ 24×7 AWS DDoS Response Team (DRT)

✔ Cost protection for scaling caused by DDoS events

✔ Detailed attack visibility

✔ Enhanced monitoring

Suitable for:

- Banking
- Healthcare
- Government
- Enterprise applications
- Large e-commerce platforms

---

# Common DDoS Attacks

AWS Shield helps protect against:

- SYN Flood
- UDP Flood
- Reflection Attacks
- DNS Flood
- TCP Flood
- Volumetric Attacks

For HTTP/HTTPS application-layer attacks, AWS WAF provides additional protection.

---

# AWS Shield Integration

AWS Shield works with:

```text
Internet

↓

AWS Shield

↓

CloudFront

↓

AWS WAF

↓

Application Load Balancer

↓

EC2
```

This layered approach provides stronger protection.

---

# AWS Console Navigation

```text
AWS Console

↓

AWS WAF & Shield

↓

Shield

↓

Protected Resources
```

---

# AWS CLI

List protections:

```bash
aws shield list-protections
```

Describe protection:

```bash
aws shield describe-protection \
--protection-id protection-id
```

List attacks:

```bash
aws shield describe-attack \
--attack-id attack-id
```

---

# Monitoring

AWS Shield integrates with:

- Amazon CloudWatch
- AWS CloudTrail
- AWS Health Dashboard

Monitor:

- DDoS events
- Traffic volume
- Attack duration
- Protected resources

---

# DevOps Use Cases

AWS Shield is used for:

✔ Public websites

✔ APIs

✔ Banking applications

✔ E-commerce platforms

✔ Gaming platforms

✔ Government portals

✔ SaaS products

✔ Enterprise applications

---

# Best Practices

✔ Enable CloudFront

✔ Use AWS WAF together with Shield

✔ Enable CloudWatch monitoring

✔ Use Auto Scaling

✔ Protect public Load Balancers

✔ Keep applications in multiple Availability Zones

✔ Use Route 53 health checks

---

# Troubleshooting

## Website Slow During Traffic Spike

Check:

- CloudFront
- Auto Scaling
- CloudWatch metrics
- AWS Shield dashboard

---

## Application Under Attack

Verify:

- Shield protection
- WAF rules
- CloudFront distribution
- Health checks

---

## High Traffic but Normal Users

Differentiate between:

- Marketing campaign
- Flash sale
- DDoS attack

Use CloudWatch metrics and AWS Shield dashboards.

---

# 🏢 Real Production Scenario

## Secure E-Commerce Platform

```text
                    Users

                      │

                  Route 53

                      │

                CloudFront

                      │

                 AWS Shield

                      │

                  AWS WAF

                      │

          Application Load Balancer

                      │

           Auto Scaling Group

          ┌───────────┼───────────┐

          │           │           │

        EC2-A       EC2-B      EC2-C

                      │

                 Amazon RDS
```

### Request Flow

1. Users access the website through Route 53.
2. CloudFront serves cached content from edge locations.
3. AWS Shield automatically detects and mitigates DDoS attacks.
4. AWS WAF inspects HTTP/HTTPS requests and blocks malicious traffic.
5. The Application Load Balancer distributes requests across healthy EC2 instances.
6. Auto Scaling adds or removes EC2 instances based on traffic demand.
7. Application data is stored securely in Amazon RDS.

Benefits:

✔ DDoS Protection

✔ High Availability

✔ Global Performance

✔ Automatic Scaling

✔ Secure Web Applications

---

# AWS Shield vs AWS WAF

| Feature | AWS Shield | AWS WAF |
|----------|------------|----------|
| Purpose | DDoS Protection | Web Application Firewall |
| Layer | Layer 3 & 4 (Standard) | Layer 7 |
| SQL Injection Protection | No | Yes |
| XSS Protection | No | Yes |
| DDoS Protection | Yes | Limited (Application Layer) |
| Best Used With | WAF + CloudFront | Shield + CloudFront |

---

# Interview Questions

### What is AWS Shield?

AWS Shield is a managed DDoS protection service that protects AWS resources from network and transport layer attacks.

---

### What is the difference between Shield Standard and Shield Advanced?

Shield Standard provides automatic protection against common network-layer DDoS attacks.

Shield Advanced adds enhanced detection, cost protection, detailed reporting, and access to the AWS DDoS Response Team (DRT).

---

### Is AWS Shield free?

Shield Standard is included at no additional cost.

Shield Advanced is a paid service.

---

### Does AWS Shield replace AWS WAF?

No.

AWS Shield protects against DDoS attacks, while AWS WAF protects web applications from application-layer attacks such as SQL Injection and Cross-Site Scripting (XSS).

---

# Screenshot

```text
screenshots/

└── shield/

    ├── shield-dashboard.png
    ├── protected-resources.png
    ├── attack-dashboard.png
    └── shield-complete-lab.png
```

---

# Official AWS References

- AWS Shield Developer Guide
- AWS WAF Developer Guide
- AWS DDoS Resiliency Best Practices
- AWS Well-Architected Framework
- AWS CLI Command Reference

---

# Quick Revision

```text
AWS Shield → DDoS Protection

Shield Standard → Free

Shield Advanced → Paid

Protects → CloudFront, Route 53, ALB, NLB

Best Used With → AWS WAF + CloudFront
```

---

# Skills Covered

✔ AWS Shield

✔ DDoS Protection

✔ Shield Standard

✔ Shield Advanced

✔ CloudFront Integration

✔ High Availability

✔ Production Security

---

# Status

AWS Shield Completed 🛡️🚀
