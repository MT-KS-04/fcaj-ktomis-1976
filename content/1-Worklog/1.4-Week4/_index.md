---
title: "Week 4 Worklog"
date: 2026-05-25
weight: 4
chapter: false
pre: " <b> 4.1. </b> "
---

### Week 4 Goals:

- Understand the process and tools for migrating servers and databases to AWS.
- Learn disaster recovery strategies.
- Know how to manage operations with Systems Manager and organize resources with Tags.

### Activities Implemented During the Week:

| Day | Activities                                                                                                                                                                                                                                                            | Start Date | Completion Date | Reference                          |
| --- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------- | --------------- | ---------------------------------- |
| 2   | - Explored AWS VM Import/Export: <br>&emsp; + Supported VM formats <br>&emsp; + The role of S3 and IAM Role during import <br>&emsp; + The process of importing an image as an AMI                                                                                    | 25/05/2026 | 25/05/2026      | <https://000014.awsstudygroup.com> |
| 3   | - Explored AWS DMS and Schema Conversion Tool (SCT): <br>&emsp; + Homogeneous vs Heterogeneous migration <br>&emsp; + Full load and CDC (Change Data Capture) <br>&emsp; + The role of SCT <br> - **Hands-on:** <br>&emsp; + Configured a basic replication task      | 26/05/2026 | 26/05/2026      | <https://000043.awsstudygroup.com> |
| 4   | - Explored AWS Elastic Disaster Recovery: <br>&emsp; + RPO and RTO concepts <br>&emsp; + Continuous replication mechanism <br>&emsp; + Failover / failback process                                                                                                    | 27/05/2026 | 27/05/2026      | <https://000100.awsstudygroup.com> |
| 5   | - Explored AWS Systems Manager: <br>&emsp; + Parameter Store <br>&emsp; + Run Command <br>&emsp; + Patch Manager, Inventory <br> - **Hands-on:** <br>&emsp; + Managed an EC2 instance via Systems Manager <br>&emsp; + Saved and read parameters with Parameter Store | 28/05/2026 | 28/05/2026      | <https://000031.awsstudygroup.com> |
| 6   | - Explored Systems Manager Session Manager: <br>&emsp; + Accessing EC2 without SSH, without opening port 22 <br>&emsp; + The role of IAM Role and SSM Agent <br> - **Hands-on:** <br>&emsp; + Opened a session into EC2 via Session Manager                           | 29/05/2026 | 29/05/2026      | <https://000058.awsstudygroup.com> |
| 7   | - Explored Tags and Resource Groups: <br>&emsp; + Tagging strategy <br>&emsp; + The role of tags in cost allocation <br> - **Hands-on:** <br>&emsp; + Tagged resources <br>&emsp; + Created a Resource Group by tag                                                   | 30/05/2026 | 30/05/2026      | <https://000027.awsstudygroup.com> |

### Achievements During Week 4:

- Understood the process for migrating servers to AWS with VM Import/Export:
  - Supported VM formats
  - The role of S3 and IAM Role in the import process
  - The process of converting a VM image to an AMI

- Learned how to migrate databases with AWS DMS:
  - Distinguished homogeneous and heterogeneous migration
  - The role of the Schema Conversion Tool when changing engines
  - Understood how full load and CDC reduce downtime during migration

- Learned disaster recovery strategy with Elastic Disaster Recovery:
  - Distinguished RPO (maximum acceptable data loss) and RTO (recovery time)
  - The continuous replication mechanism
  - The failover and failback process

- Learned centralized administration with AWS Systems Manager:
  - Stored configuration with Parameter Store (String and SecureString)
  - Executed remote commands with Run Command
  - Patched and inventoried with Patch Manager, Inventory

- Securely accessed servers with Session Manager:
  - No key pair needed, no need to open port 22
  - Understood the requirements: IAM Role `AmazonSSMManagedInstanceCore` and SSM Agent
  - Compared the security advantages over traditional SSH

- Organized resources effectively with Tags and Resource Groups:
  - Built a consistent tagging strategy
  - Grouped resources by tag
  - Used tags for cost allocation
