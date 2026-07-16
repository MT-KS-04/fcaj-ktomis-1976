---
title: "Week 2 Worklog"
date: 2026-05-11
weight: 2
chapter: false
pre: " <b> 2.1. </b> "
---

### Week 2 Goals:

- Learn about relational databases on AWS with Amazon RDS.
- Understand simplification solutions (Lightsail) and elasticity (Auto Scaling).
- Know how to monitor systems with CloudWatch and manage DNS with Route 53.

### Activities Implemented During the Week:

| Day | Activities                                                                                                                                                                                                                                                                                                          | Start Date | Completion Date | Reference                                                                  |
| --- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------- | --------------- | -------------------------------------------------------------------------- |
| 2   | - Explored Amazon RDS: <br>&emsp; + Supported database engines <br>&emsp; + Multi-AZ <br>&emsp; + Read Replica <br> - **Hands-on:** <br>&emsp; + Launched an RDS instance in a private subnet <br>&emsp; + Connected to RDS from an EC2 instance in the same VPC <br>&emsp; + Configured the Security Group for RDS | 11/05/2026 | 11/05/2026      | <https://000005.awsstudygroup.com>                                         |
| 3   | - Explored Amazon Lightsail and its use cases <br> - Explored Lightsail Containers <br> - Compared Lightsail with EC2 <br> - **Hands-on:** <br>&emsp; + Created a Lightsail instance with a sample application                                                                                                      | 12/05/2026 | 12/05/2026      | <https://000045.awsstudygroup.com> <br> <https://000046.awsstudygroup.com> |
| 4   | - Explored EC2 Auto Scaling: <br>&emsp; + Auto Scaling Group <br>&emsp; + Launch Template <br>&emsp; + Scaling policies (target tracking, step, scheduled) <br> - **Hands-on:** <br>&emsp; + Configured an ASG with min/max/desired capacity                                                                        | 13/05/2026 | 13/05/2026      | <https://000006.awsstudygroup.com>                                         |
| 5   | - Explored Amazon CloudWatch: <br>&emsp; + Metrics, Alarms <br>&emsp; + Logs, Dashboards <br> - **Hands-on:** <br>&emsp; + Created an alarm for high CPU usage <br>&emsp; + Linked the alarm to Auto Scaling                                                                                                        | 14/05/2026 | 14/05/2026      | <https://000008.awsstudygroup.com>                                         |
| 6   | - Explored Amazon Route 53: <br>&emsp; + Record types (A, CNAME, Alias) <br>&emsp; + Routing policies (simple, weighted, latency, failover) <br>&emsp; + Health checks <br> - **Hands-on:** <br>&emsp; + Created a hosted zone and configured records                                                               | 15/05/2026 | 15/05/2026      | <https://000010.awsstudygroup.com>                                         |
| 7   | - Explored AWS Cloud9 (cloud-based IDE) <br> - **Hands-on:** <br>&emsp; + Created a Cloud9 environment <br>&emsp; + Used the integrated terminal to run AWS CLI commands <br> - Summarized Week 2 knowledge                                                                                                         | 16/05/2026 | 16/05/2026      | <https://000049.awsstudygroup.com>                                         |

### Achievements During Week 2:

- Learned about managed databases on AWS with Amazon RDS:
  - Supported database engines
  - The role of Multi-AZ in ensuring availability
  - The role of Read Replica in scaling reads
  - Launched RDS in a private subnet and connected from EC2

- Understood Amazon Lightsail as a simplification option:
  - Cases where Lightsail is a better fit than EC2
  - Lightsail Containers for running containers without infrastructure management

- Learned the auto-scaling mechanism with EC2 Auto Scaling:
  - Auto Scaling Group and Launch Template
  - Distinguished the various scaling policy types
  - Configured min/max/desired capacity

- Learned how to monitor systems with Amazon CloudWatch:
  - Created and read Metrics
  - Configured threshold-based Alarms
  - Collected Logs
  - Built Dashboards
  - Linked alarms to Auto Scaling to trigger scaling actions

- Learned how to manage DNS with Amazon Route 53:
  - Distinguished record types
  - Understood routing policies and their use cases
  - The role of health checks

- Got familiar with the AWS Cloud9 development environment and its benefits when coding in an environment with AWS CLI pre-installed.
- Understood the relationships between services when combined: RDS in a private subnet, EC2 access via Security Group, Auto Scaling coordinating with CloudWatch.
