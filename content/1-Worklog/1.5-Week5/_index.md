---
title: "Week 5 Worklog"
date: 2026-06-01
weight: 5
chapter: false
pre: " <b> 5.1. </b> "
---

## General Information

| Content         | Details                                                                              |
| --------------- | ------------------------------------------------------------------------------------ |
| Duration        | 06/01/2026 - 06/07/2026                                                              |
| Internship Week | Week 5                                                                               |
| Phase           | Optimize - Operations & Cost Optimization                                            |
| Program         | First Cloud Journey                                                                  |
| Main Topics     | Infrastructure as Code, quota management, cost management, and resource optimization |
| Weekly Goals    | Master CloudFormation, AWS CDK, Service Quotas, Cost Management, EC2 Optimization    |

## Week 5 Learning Orientation

Week 5 continues the **Optimize** phase with two areas: **Infrastructure as Code** (CloudFormation, AWS CDK) and **cost and resource optimization** (Service Quotas, Cost and Usage Management, EC2 Resource Optimization, VPC Flow Logs). IaC is a new and challenging area for me, so I dedicated the first two days to CloudFormation and CDK, leaving the lighter cost and monitoring topics for the subsequent days.

## Week 5 Learning Objectives

- Explore Infrastructure as Code with AWS CloudFormation.
- Explore Cloud Development Kit (AWS CDK) Essentials.
- Explore Managing Quotas with Service Quotas.
- Explore Cost and Usage Management.
- Explore Right-Sizing with EC2 Resource Optimization.
- Explore Network Monitoring with VPC Flow Logs.

## Activities Implemented During the Week

### Day 1 - Monday, 06/01/2026

Topic: **Infrastructure as Code with AWS CloudFormation**.
Implemented Activities:

- Read about the concept of Infrastructure as Code and why it's beneficial.
- Learned about template structures: Resources, Parameters, Outputs, and the concepts of stacks and change sets.
- Followed a workshop: modified a sample template and deployed it to see it automatically create resources.

Deployed a stack from a template file:

```bash
aws cloudformation deploy \
  --template-file s3-bucket.yaml \
  --stack-name intern-demo-stack
```

The first attempt resulted in an error due to incorrect indentation (YAML is very strict about this):

```
Template format error: [/Resources] 'null' values are not allowed in templates
```

Fixed the indentation and deployed successfully:

```
Successfully created/updated stack - intern-demo-stack
```

Checked the resources created by the stack:

```bash
aws cloudformation describe-stack-resources \
  --stack-name intern-demo-stack \
  --query "StackResources[].ResourceType" --output text
```

Achieved Results:

- Understood the benefits of IaC compared to manual console configurations.
- Successfully deployed a simple stack from a template.
- Learned that CloudFormation's YAML is highly sensitive to indentation; a small mistake breaks the entire template.

### Day 2 - Tuesday, 06/02/2026

Topic: **Cloud Development Kit (AWS CDK) Essentials**.
Implemented Activities:

- Read about CDK and how to write infrastructure using programming languages instead of YAML/JSON.
- Explored constructs, stacks, and apps, and compared them to raw CloudFormation.
- Followed a guide to initialize a CDK project and synthesize it into a template.

Initialized a project and synthesized CloudFormation:

```bash
cdk init app --language typescript
cdk synth
```

During the deployment step, I was blocked:

```
This stack uses assets, so the toolkit stack must be deployed to the environment (Run "cdk bootstrap ...")
```

It turned out the account hadn't been bootstrapped. I had to run this command once for the current region before I could deploy:

```bash
cdk bootstrap aws://123456789012/ap-southeast-1
cdk deploy
```

Achieved Results:

- Understood that CDK allows for writing more concise and reusable infrastructure code.
- Successfully ran the initialization - synth - deploy cycle at a basic level.
- Memorized that a new account requires a one-time `cdk bootstrap` before deploying, otherwise it will be blocked.

### Day 3 - Wednesday, 06/03/2026

Topic: **Managing Quotas with Service Quotas**.
Implemented Activities:

- Read about Service Quotas and the significance of service limits.
- Learned how to check current quotas and the process for requesting increases.
- Navigated to the Service Quotas dashboard to review limits for a few active services.

Achieved Results:

- Understood how quotas impact system scalability.
- Knew where to check and request quota increases when necessary.

### Day 4 - Thursday, 06/04/2026

Topic: **Cost and Usage Management**.
Implemented Activities:

- Read about tracking and analyzing costs and usage.
- Explored Cost Explorer and Cost and Usage Reports.
- Accessed Cost Explorer to view cost graphs and filter them by tags.

Achieved Results:

- Learned how to use Cost Explorer to observe cost trends.
- Understood how tags assist in allocating costs by groups.

### Day 5 - Friday, 06/05/2026

Topic: **Right-Sizing with EC2 Resource Optimization**.
Implemented Activities:

- Read about right-sizing and how to use metrics to select appropriate instance types.
- Explored tools that provide optimization recommendations.
- Reviewed metrics for an instance to understand when resizing is needed.

Achieved Results:

- Understood that right-sizing saves costs while maintaining performance.
- Knew how to rely on data for decisions instead of choosing instances based on intuition.

### Day 6 - Saturday, 06/06/2026

Topic: **Network Monitoring with VPC Flow Logs**.
Implemented Activities:

- Read about VPC Flow Logs and the structure of a log record.
- Followed a guide to enable flow logs and push them to CloudWatch Logs.
- Reviewed a few records to understand how to read and filter by ACCEPT/REJECT.
- Summarized the knowledge from the entire week.

Achieved Results:

- Successfully enabled flow logs and read basic records.
- Understood that flow logs are used for connectivity troubleshooting and security auditing.

## Week 5 Knowledge Summary

| Knowledge Group        | Learned Content                                       |
| ---------------------- | ----------------------------------------------------- |
| Infrastructure as Code | CloudFormation (template, stack), AWS CDK (construct) |
| Quotas                 | Service Quotas                                        |
| Cost Management        | Cost and Usage Management, Cost Explorer              |
| Optimization           | EC2 Resource Optimization (right-sizing)              |
| Network Monitoring     | VPC Flow Logs                                         |

## Achievements During the Week

- Successfully deployed infrastructure using CloudFormation and CDK.
- Knew how to check Service Quotas.
- Viewed and analyzed costs using Cost Explorer.
- Understood how to right-size EC2 resources.
- Enabled and read VPC Flow Logs.

## Challenges Encountered

- CloudFormation template syntax looked daunting initially; I had to start with a sample file and modify it block by block rather than writing from scratch.
- CDK requires environment setup and bootstrapping; I got stuck here for a bit, encountering errors until I precisely followed the guide.
- Flow logs generate an overwhelming number of lines; I had to filter by REJECT and specific IPs to find relevant information.

## Lessons Learned

- After learning IaC, I realized that while manual console setup is fast, it's hard to replicate. Writing it as code ensures exact reproducibility.
- CDK suits me better because I can write in a familiar programming language, saving me from remembering YAML syntax.
- Cost optimization is not just about looking at bills; it ties into tagging, right-sizing, and actively reviewing metrics.

## Plan for Week 6

- Transition to Optimize - Security: IAM Permission Boundaries, IAM Policies and Conditions.
- Explore KMS, Secrets Manager, AWS WAF, Security Hub.

## End of Week Review

The IaC part of Week 5 was the most exhausting, but it was also the most valuable because it completely shifted how I think about building infrastructure. The cost and monitoring sections were lighter, serving to balance things out after two intense days.
