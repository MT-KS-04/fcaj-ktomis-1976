---
title: "Week 2 Worklog"
date: 2026-05-10
weight: 2
chapter: false
pre: " <b> 2.1. </b> "
---

## General Information

| Content         | Details                                                                           |
| --------------- | --------------------------------------------------------------------------------- |
| Duration        | 05/10/2026 - 05/16/2026                                                           |
| Internship Week | Week 2                                                                            |
| Phase           | Explore AWS Services                                                              |
| Program         | First Cloud Journey                                                               |
| Main Topics     | Databases, Lightsail, Auto Scaling, monitoring, DNS, and development environments |
| Weekly Goals    | Master RDS, Lightsail, EC2 Auto Scaling, CloudWatch, Route 53, and Cloud9         |

## Week 2 Learning Orientation

Continuing the **Explore AWS Services** phase, week 2 covered extended services based on the existing foundation: relational databases (RDS), simplified solutions (Lightsail), elasticity (EC2 Auto Scaling), monitoring (CloudWatch), DNS (Route 53), and cloud development environments (Cloud9). I still followed the approach of reading the easier topics first and leaving the ones that require more hands-on configuration for later, tackling a maximum of 1-2 services per day.

## Week 2 Learning Objectives

- Explore Amazon RDS (Relational Database Service).
- Explore Amazon Lightsail and Lightsail Containers.
- Explore Scaling Applications with EC2 Auto Scaling.
- Explore Monitoring with Amazon CloudWatch.
- Explore Hybrid DNS Management with Amazon Route 53.
- Explore Cloud Development with AWS Cloud9.

## Activities Implemented During the Week

### Day 1 - Monday, 05/11/2026

Topic: **Database Essentials with Amazon RDS**.
Implemented Activities:

- Read RDS documentation: supported database engines, the concepts of Multi-AZ and Read Replicas.
- Followed a workshop to create an RDS instance in a private subnet.
- Tested connecting to RDS from an EC2 instance within the same VPC to observe the connection flow.

Retrieved the RDS endpoint via CLI and connected from EC2 (using PostgreSQL):

```bash
aws rds describe-db-instances \
  --query "DBInstances[].Endpoint.Address" --output text
```

```
intern-db.abcdefg123.ap-southeast-1.rds.amazonaws.com
```

```bash
psql -h intern-db.abcdefg123.ap-southeast-1.rds.amazonaws.com -U postgres -d postgres
```

The first time, I tried connecting from my personal machine, and it hung and timed out. I later realized that RDS was in a private subnet, meaning I had to SSH into an EC2 instance in the same VPC before connecting. Moreover, the RDS Security Group had to allow port 5432 for the EC2 Security Group.

Achieved Results:

- Understood how RDS differs from manually installing a database on EC2.
- Grasped the meaning of Multi-AZ (redundancy) and Read Replicas (read scalability), albeit at a theoretical level.
- Memorized that accessing a private RDS requires routing through a machine in the VPC and cannot be connected directly from the outside.

### Day 2 - Tuesday, 05/12/2026

Topic: **Simplified Computing with Amazon Lightsail** and **Container Deployment with Amazon Lightsail Containers**.
Implemented Activities:

- Read about Lightsail and when it's a better fit than EC2 (small apps, desire for simplicity).
- Followed a guide to create a Lightsail instance with a sample application.
- Read more about Lightsail Containers to know how to run containers without worrying about infrastructure.

Achieved Results:

- Understood when to choose Lightsail over EC2.
- Knew of the existence of Lightsail Containers and the problems they solve.

### Day 3 - Wednesday, 05/13/2026

Topic: **Scaling Applications with EC2 Auto Scaling**.
Implemented Activities:

- Read about Auto Scaling Groups and Launch Templates.
- Explored scaling policies: target tracking, step scaling, scheduled scaling.
- Followed a workshop to configure an ASG with min/max/desired capacities to observe how it scales.

Achieved Results:

- Understood the concept behind Auto Scaling and why it helps save costs.
- Gained a preliminary understanding of the different scaling policies.

### Day 4 - Thursday, 05/14/2026

Topic: **Monitoring with Amazon CloudWatch**.
Implemented Activities:

- Read about CloudWatch: Metrics, Alarms, Logs, Dashboards.
- Followed a guide to create a CPU high alert alarm.
- Learned how this alarm integrates with Auto Scaling to trigger scaling actions.

Achieved Results:

- Knew what CloudWatch monitors and how to create an alarm.
- Understood the connection between CloudWatch and Auto Scaling.

### Day 5 - Friday, 05/15/2026

Topic: **Hybrid DNS Management with Amazon Route 53**.
Implemented Activities:

- Read about Route 53: record types (A, CNAME, Alias) and routing policies.
- Learned about health checks and routing methods (simple, weighted, latency, failover).
- Reviewed a guide on creating a hosted zone and pointing a record to an AWS resource.

Achieved Results:

- Understood Route 53's role in domain management.
- Gained a basic understanding of routing policies and when to use them.

### Day 6 - Saturday, 05/16/2026

Topic: **Cloud Development with AWS Cloud9**.
Implemented Activities:

- Read about Cloud9 as a cloud-based IDE.
- Created a Cloud9 environment and opened the integrated terminal to run a few AWS CLI commands.
- Summarized the knowledge from the entire week.

Achieved Results:

- Successfully tried Cloud9 and found it convenient because AWS CLI was pre-installed.
- Understood the benefits of coding in an environment close to AWS.

## Week 2 Knowledge Summary

| Knowledge Group | Learned Content                                   |
| --------------- | ------------------------------------------------- |
| Database        | Amazon RDS, Multi-AZ, Read Replica                |
| Simplified      | Amazon Lightsail, Lightsail Containers            |
| Scalability     | EC2 Auto Scaling, Launch Template, scaling policy |
| Monitoring      | CloudWatch Metrics, Alarms, Logs, Dashboards      |
| DNS             | Route 53, record, routing policy, health check    |
| Development     | AWS Cloud9                                        |

## Achievements During the Week

- Successfully created and connected to RDS from EC2 following the workshop.
- Learned about Lightsail as a simpler alternative to EC2.
- Configured EC2 Auto Scaling and CloudWatch alarms.
- Understood how Route 53 manages DNS.
- Got familiar with the Cloud9 environment.

## Challenges Encountered

- When trying to connect to RDS from EC2, I got stuck for a while. Later, I realized the RDS Security Group and subnet group didn't allow the connection.
- After configuring Auto Scaling, it didn't scale as expected in the tutorial. I had to review the alarm and policy to realize the threshold I set was inappropriate.
- The various Route 53 routing policies had similar names, so I initially confused them. I had to write them down based on their purposes to remember.

## Lessons Learned

- I learned that keeping databases in private subnets is definitely safer, but it requires careful network configuration rather than just "creating and running."
- Auto Scaling and CloudWatch essentially go hand in hand; you must understand one to use the other.
- Lightsail is great for small workloads, but flexibility requires reverting to EC2 — there is no one-size-fits-all solution.

## Plan for Week 3

- Explore Amazon DynamoDB and Amazon ElastiCache.
- Explore Amazon CloudFront and Lambda@Edge.
- Explore the Networking on AWS Workshop.
- Practice Building Highly Available Web Applications.

## End of Week Review

Week 2 introduced more complex topics, especially configuration-heavy ones like RDS and Auto Scaling. I found that reading first and then practicing through workshops suits me best, as many gaps in understanding only become apparent during hands-on practice.
