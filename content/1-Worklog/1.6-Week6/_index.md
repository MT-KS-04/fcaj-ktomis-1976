---
title: "Week 6 Worklog"
date: 2026-06-07
weight: 6
chapter: false
pre: " <b> 6.1. </b> "
---

## General Information

| Content         | Details                                                                                              |
| --------------- | ---------------------------------------------------------------------------------------------------- |
| Duration        | 06/07/2026 - 06/13/2026                                                                              |
| Internship Week | Week 6                                                                                               |
| Phase           | Optimize - Security                                                                                  |
| Program         | First Cloud Journey                                                                                  |
| Main Topics     | Security: advanced permissions, encryption, secret management, application protection                |
| Weekly Goals    | Master IAM Permission Boundaries, IAM Policies & Conditions, KMS, Secrets Manager, WAF, Security Hub |

## Week 6 Learning Orientation

Week 6 focused on the **Security** group within the **Optimize** phase. The content covered advanced permissions (Permission Boundaries, IAM Policies and Conditions), encryption (KMS), sensitive information management (Secrets Manager), application protection (WAF), and centralized security posture (Security Hub). I started with topics closer to the familiar IAM and progressively moved towards encryption and application protection, tackling 1-2 topics per day.

## Week 6 Learning Objectives

- Explore Permission Management with IAM Permission Boundaries.
- Explore Access Control with IAM Policies and Conditions.
- Explore Encryption with AWS Key Management Service (KMS).
- Explore Credentials Management with AWS Secrets Manager.
- Explore Application Protection with AWS WAF.
- Explore Security Compliance with AWS Security Hub.

## Activities Implemented During the Week

### Day 1 - Monday, 06/08/2026

Topic: **Permission Management with IAM Permission Boundaries**.
Implemented Activities:

- Read about Permission Boundaries and the concept of "maximum permissions" for an IAM entity.
- Distinguished between boundaries and identity-based policies.
- Followed a guide to attach a permission boundary to an IAM User.

Achieved Results:

- Understood how a boundary differs from a standard policy.
- Successfully attached a boundary to an entity based on the example.

### Day 2 - Tuesday, 06/09/2026

Topic: **Access Control with IAM Policies and Conditions**.
Implemented Activities:

- Read more deeply into policy structures: Effect, Action, Resource, and specifically, Condition.
- Explored common condition keys (IP, MFA, tags).
- Wrote a conditional policy and tested whether it blocked access as expected.

Achieved Results:

- Grasped the level of granular access control Conditions provide.
- Successfully wrote a simple conditional policy.

### Day 3 - Wednesday, 06/10/2026

Topic: **Encryption with AWS Key Management Service (KMS)**.
Implemented Activities:

- Read about KMS: CMK concepts, distinguishing between AWS managed keys and customer managed keys.
- Learned about envelope encryption.
- Followed a guide to encrypt/decrypt data and enable encryption for an S3 bucket.

Achieved Results:

- Understood how KMS manages keys and encrypts data.
- Successfully enabled encryption for S3 following the guide.

### Day 4 - Thursday, 06/11/2026

Topic: **Credentials Management with AWS Secrets Manager**.
Implemented Activities:

- Read about Secrets Manager and the secret rotation mechanism.
- Compared Secrets Manager with the Parameter Store learned in week 4.
- Practiced: stored a secret (e.g., database connection info) and retrieved it.

Stored a secret and read it via CLI:

```bash
aws secretsmanager create-secret --name intern/db-cred \
  --secret-string '{"username":"admin","password":"P@ss123"}'

aws secretsmanager get-secret-value --secret-id intern/db-cred \
  --query "SecretString" --output text
```

```json
{ "username": "admin", "password": "P@ss123" }
```

I tried recreating a secret with the same name and got:

```
An error occurred (ResourceExistsException): The operation failed because the secret intern/db-cred already exists.
```

To update the value, I had to use `put-secret-value` instead of `create-secret` — this was my mistake.

Achieved Results:

- Understood that Secrets Manager helps manage credentials more securely than keeping them in code.
- Successfully stored and read a basic secret.
- Distinguished between `create-secret` (for creation) and `put-secret-value` (for updates).

### Day 5 - Friday, 06/12/2026

Topic: **Application Protection with AWS WAF**.
Implemented Activities:

- Read about WAF and how it blocks common web attacks (SQL injection, XSS, rate limiting).
- Explored Web ACLs, rules, and rule groups.
- Followed a guide to create a Web ACL with basic rules and attached it to CloudFront/ALB.

Achieved Results:

- Understood which layer WAF protects web applications at.
- Successfully configured a simple Web ACL.

### Day 6 - Saturday, 06/13/2026

Topic: **Security Compliance with AWS Security Hub**.
Implemented Activities:

- Read about Security Hub and how it centralizes security posture.
- Learned about security standards and findings.
- Enabled Security Hub and reviewed the findings it reported.
- Summarized the knowledge from the entire week and the past 6 weeks.

Achieved Results:

- Grasped how Security Hub provides a holistic security view.
- Was able to read findings and prioritize them based on severity.

## Week 6 Knowledge Summary

| Knowledge Group      | Learned Content                              |
| -------------------- | -------------------------------------------- |
| Permission           | IAM Permission Boundaries                    |
| Access Control       | IAM Policies and Conditions                  |
| Encryption           | KMS, CMK, envelope encryption                |
| Secrets              | Secrets Manager, rotation                    |
| Application Security | AWS WAF, Web ACL, rule                       |
| Compliance           | AWS Security Hub, security standard, finding |

## Achievements During the Week

- Understood and successfully attached permission boundaries, and wrote policies with conditions.
- Enabled data encryption using KMS.
- Stored and managed secrets with Secrets Manager.
- Configured WAF to protect a web application.
- Enabled and reviewed findings in Security Hub.

## Challenges Encountered

- Initially, I thought permission boundaries and standard policies were the same. Careful reading clarified that boundaries only limit maximum permissions without granting them.
- There are too many condition keys in policies to remember them all, so I started getting familiar with simple ones like IP and MFA.
- Envelope encryption felt abstract on paper; I had to draw out data keys and master keys to visualize how they nest together.

## Lessons Learned

- Finishing this week, I realized security isn't localized; it's spread across multiple layers: permissions, encryption, application protection, and overall monitoring.
- Storing passwords or keys in code is a bad habit; with Secrets Manager available, it should be abandoned completely.
- Security Hub is convenient for centralizing everything into one dashboard, but the volume of findings requires prioritization instead of trying to address them all at once.

## 6-Week Summary

Over these 6 weeks, I have covered most of the major sections of the First Cloud Journey: **Explore AWS Services** (weeks 1–3), **Migrate to AWS** and the beginning of **Optimize** (week 4), continuing with **Optimize - Operations & Cost** (week 5), and **Optimize - Security** (week 6). Starting from scratch, I now possess a solid foundational understanding of accounts, networking, compute, storage, databases, migration, IaC, cost management, and security.

## End of Week Review

Week 6 wrapped up the first 6 weeks with the security topics, which required the most careful and deliberate reading. Looking back over the entire journey, the approach of progressing from easy to difficult and tackling only 1-2 services a day prevented me from feeling overwhelmed, ensuring I understood each topic solidly rather than rushing through them.
