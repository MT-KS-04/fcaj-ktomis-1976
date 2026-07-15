---
title: "Week 4 Worklog"
date: 2026-05-25
weight: 4
chapter: false
pre: " <b> 4.1. </b> "
---

## General Information

| Content         | Details                                                                              |
| --------------- | ------------------------------------------------------------------------------------ |
| Duration        | 05/25/2026 - 05/31/2026                                                              |
| Internship Week | Week 4                                                                               |
| Phase           | Migrate to AWS & Optimize - Operations                                               |
| Program         | First Cloud Journey                                                                  |
| Main Topics     | Server and database migration, disaster recovery, operations management              |
| Weekly Goals    | Master VM Import/Export, DMS + SCT, Elastic Disaster Recovery, Systems Manager, Tags |

## Week 4 Learning Orientation

Week 4 transitions into the **Migrate to AWS** phase and begins the **Optimize - Operations** section. The content revolves around server migration tools (VM Import/Export), database migration (DMS + SCT), disaster recovery (Elastic Disaster Recovery), and operations management tools (Systems Manager, Session Manager, Tags & Resource Groups). The migration and DR sections were quite abstract and difficult to simulate fully, so this week leaned towards understanding the processes rather than extensive hands-on practice.

## Week 4 Learning Objectives

- Explore VM Migration with AWS VM Import/Export.
- Explore Database Migration with AWS DMS and Schema Conversion Tool (SCT).
- Explore Disaster Recovery with AWS Elastic Disaster Recovery.
- Explore Systems Management with AWS Systems Manager.
- Explore Remote Server Access with Systems Manager Session Manager.
- Explore Resource Organization with Tags and Resource Groups.

## Activities Implemented During the Week

### Day 1 - Monday, 05/25/2026

Topic: **VM Migration with AWS VM Import/Export**.
Implemented Activities:

- Read about VM Import/Export and how to bring existing VMs to AWS.
- Learned about supported VM formats and the roles of S3 and IAM Roles during the import process.
- Read through a step-by-step workshop to visualize the process of importing an image into an AMI (mainly reading because I didn't have a source VM to practice with).

Achieved Results:

- Understood the procedural flow of migrating an on-premise VM to AWS.
- Knew the format and permission prerequisites for an import.

### Day 2 - Tuesday, 05/26/2026

Topic: **Database Migration with AWS DMS and Schema Conversion Tool (SCT)**.
Implemented Activities:

- Read about DMS and distinguished between homogeneous and heterogeneous migrations.
- Learned about the role of SCT when converting schemas between different engines.
- Explored full load and CDC modes.
- Followed a guide to configure a basic replication task.

Achieved Results:

- Understood how DMS moves data and how CDC helps reduce downtime.
- Knew when to incorporate SCT.

### Day 3 - Wednesday, 05/27/2026

Topic: **Disaster Recovery with AWS Elastic Disaster Recovery**.
Implemented Activities:

- Read about Elastic Disaster Recovery and the two critical concepts: RPO and RTO.
- Learned about continuous replication mechanisms and the failover/failback processes.
- Read a workshop to visualize setting up DR for a source server.

Achieved Results:

- Understood the purpose of DR and why RPO/RTO dictate the design.
- Grasped the theoretical failover flow.

### Day 4 - Thursday, 05/28/2026

Topic: **Systems Management with AWS Systems Manager**.
Implemented Activities:

- Read about Systems Manager and components like Parameter Store, Run Command, Patch Manager, and Inventory.
- Followed a guide to manage an EC2 instance via Systems Manager.
- Tested saving and reading a parameter in the Parameter Store.

Saved a parameter and retrieved it via CLI:

```bash
aws ssm put-parameter --name "/intern/db-host" \
  --value "intern-db.internal" --type String

aws ssm get-parameter --name "/intern/db-host" \
  --query "Parameter.Value" --output text
```

```
intern-db.internal
```

For sensitive information, the guide used `--type SecureString`, and reading it required `--with-decryption` to get the actual value — I forgot this the first time, and it returned an encrypted string, which looked like an error.

Achieved Results:

- Understood that Systems Manager centralizes many management tasks.
- Successfully used the Parameter Store and Run Command at a basic level.
- Memorized that reading a SecureString requires `--with-decryption`.

### Day 5 - Friday, 05/29/2026

Topic: **Remote Server Access with Systems Manager Session Manager**.
Implemented Activities:

- Read about Session Manager and how to access EC2 without SSH or opening port 22.
- Learned about the role of IAM Roles and the SSM Agent.
- Followed a guide to open a session into an EC2 instance via Session Manager.

Started a session via CLI (no key pair needed, no port 22 open):

```bash
aws ssm start-session --target i-0abc123def456
```

The first time I ran it, I got:

```
An error occurred (TargetNotConnected) when calling StartSession operation: i-0abc123def456 is not connected.
```

Upon checking, I realized the instance didn't have the IAM Role with the `AmazonSSMManagedInstanceCore` policy attached, so the SSM Agent couldn't "report" in. After attaching the role and waiting a bit, I was able to access the terminal directly in the browser/CLI.

Achieved Results:

- Accessed the instance without a key pair or opening ports, finding it more convenient and secure than SSH.
- Understood why this method is more secure.
- Memorized the prerequisites for Session Manager: the instance must have the `AmazonSSMManagedInstanceCore` role and an active SSM Agent.

### Day 6 - Saturday, 05/30/2026

Topic: **Resource Organization with Tags and Resource Groups**.
Implemented Activities:

- Read about tagging strategies and how to group resources with Resource Groups.
- Learned the role of tags in cost allocation and management.
- Practiced: attached tags to a few resources and created a Resource Group based on tags.
- Summarized the knowledge from the entire week.

Achieved Results:

- Knew how to organize resources more cleanly using tags.
- Successfully created a simple Resource Group.

## Week 4 Knowledge Summary

| Knowledge Group    | Learned Content                               |
| ------------------ | --------------------------------------------- |
| Server Migration   | VM Import/Export                              |
| Database Migration | DMS, SCT, full load, CDC                      |
| Disaster Recovery  | Elastic Disaster Recovery, RPO, RTO, failover |
| Operations         | Systems Manager, Parameter Store, Run Command |
| Remote Access      | Session Manager                               |
| Organization       | Tags and Resource Groups                      |

## Achievements During the Week

- Understood the process of migrating servers and databases to AWS.
- Grasped the core concepts and ideas behind disaster recovery.
- Successfully used Systems Manager and Session Manager.
- Knew how to organize resources using tags and Resource Groups.

## Challenges Encountered

- VM Import/Export and DR felt a bit "dry" this week because I lacked an actual source system to migrate. I primarily read about the processes and visualized them rather than completing end-to-end setups.
- RPO and RTO were confusing initially. I had to use specific examples like "maximum data loss acceptable" and "time to recovery" to distinguish them clearly.
- Session Manager refused to connect initially. I later found out the IAM Role was missing and the SSM Agent wasn't ready.

## Lessons Learned

- Topics like migration and DR are easy to nod along with while reading, but hands-on implementation likely involves many unforeseen issues, so I can only claim to understand the processes.
- DR isn't just a switch you turn on; it must be designed around specific RPO/RTO requirements.
- Session Manager is fantastic—accessing machines without opening ports or managing keys is something I'll definitely use a lot moving forward.

## Plan for Week 5

- Continue Optimize - Operations: CloudFormation, AWS CDK, Service Quotas.
- Explore Cost and Usage Management, EC2 Resource Optimization, VPC Flow Logs.

## End of Week Review

Week 4 leaned heavily towards reading and understanding processes rather than hands-on clicking, as simulating migration and DR in a learning environment is challenging. However, Systems Manager and Session Manager were practical and actionable, and I see myself using them frequently in the future.
