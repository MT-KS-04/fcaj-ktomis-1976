---
title: "Week 6 Worklog"
date: 2026-06-08
weight: 6
chapter: false
pre: " <b> 6.1. </b> "
---

### Week 6 Goals:

- Learn advanced permission mechanisms: Permission Boundaries, Policies & Conditions.
- Understand how to encrypt data with KMS and manage sensitive information with Secrets Manager.
- Know how to protect web applications with AWS WAF and monitor security with Security Hub.

### Activities Implemented During the Week:

| Day | Activities                                                                                                                                                                                                                                                                                   | Start Date | Completion Date | Reference                          |
| --- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------- | --------------- | ---------------------------------- |
| 2   | - Explored IAM Permission Boundaries: <br>&emsp; + The concept of a maximum permission limit <br>&emsp; + Distinguished a boundary from an identity-based policy <br> - **Hands-on:** <br>&emsp; + Attached a permission boundary to an IAM User                                             | 08/06/2026 | 08/06/2026      | <https://000030.awsstudygroup.com> |
| 3   | - Explored IAM Policies and Conditions: <br>&emsp; + The structure of Effect, Action, Resource, Condition <br>&emsp; + Common condition keys (IP, MFA, tag) <br> - **Hands-on:** <br>&emsp; + Wrote a conditional policy and verified it worked                                              | 09/06/2026 | 09/06/2026      | <https://000044.awsstudygroup.com> |
| 4   | - Explored AWS KMS: <br>&emsp; + Customer Master Key (CMK) <br>&emsp; + AWS managed key vs customer managed key <br>&emsp; + Envelope encryption <br> - **Hands-on:** <br>&emsp; + Encrypted/decrypted data <br>&emsp; + Enabled encryption for an S3 bucket                                 | 10/06/2026 | 10/06/2026      | <https://000033.awsstudygroup.com> |
| 5   | - Explored AWS Secrets Manager: <br>&emsp; + Storing sensitive information <br>&emsp; + Rotation mechanism <br>&emsp; + Compared with Parameter Store <br> - **Hands-on:** <br>&emsp; + Stored and retrieved a secret via CLI <br>&emsp; + Distinguished create-secret from put-secret-value | 11/06/2026 | 11/06/2026      | <https://000096.awsstudygroup.com> |
| 6   | - Explored AWS WAF: <br>&emsp; + Web ACL, rule, rule group <br>&emsp; + Blocking SQL injection, XSS <br>&emsp; + Rate limiting <br> - **Hands-on:** <br>&emsp; + Created a Web ACL and attached it to CloudFront/ALB                                                                         | 12/06/2026 | 12/06/2026      | <https://000026.awsstudygroup.com> |
| 7   | - Explored AWS Security Hub: <br>&emsp; + Security standards <br>&emsp; + Findings and severity levels <br>&emsp; + Integration with other security services <br> - **Hands-on:** <br>&emsp; + Enabled Security Hub and reviewed findings <br> - Summarized 6 weeks of knowledge             | 13/06/2026 | 13/06/2026      | <https://000018.awsstudygroup.com> |

### Achievements During Week 6:

- Learned advanced permission mechanisms with IAM Permission Boundaries:
  - Understood that a boundary only limits the maximum permissions and does not grant permissions on its own
  - Distinguished a boundary from an identity-based policy
  - Applied it when needing to safely delegate IAM entity creation

- Controlled access in detail with IAM Policies and Conditions:
  - Mastered the structure of Effect, Action, Resource, Condition
  - Used common condition keys (IP, MFA, tag)
  - Wrote a conditional policy

- Understood and applied encryption with AWS KMS:
  - The Customer Master Key concept
  - Distinguished AWS managed key from customer managed key
  - Understood the envelope encryption mechanism (data key and master key)
  - Enabled encryption for data on S3

- Securely managed sensitive information with Secrets Manager:
  - Stored and retrieved secrets instead of hardcoding them in source code
  - Understood the automatic rotation mechanism
  - Distinguished `create-secret` (creating new) from `put-secret-value` (updating)
  - Compared it with Parameter Store

- Protected web applications with AWS WAF:
  - Configured a Web ACL with basic rules
  - Blocked common attacks: SQL injection, XSS
  - Applied rate limiting

- Monitored overall security with AWS Security Hub:
  - Understood security standards and findings
  - Learned to prioritize handling based on severity

- Understood that AWS security is multi-layered: permissions, encryption, secrets management, application protection, and overall monitoring.
- Completed the foundational learning phase, ready to move into the real project deployment phase.
