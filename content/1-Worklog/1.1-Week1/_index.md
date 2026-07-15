---
title: "Week 1 Worklog"
date: 2026-05-05
weight: 1
chapter: false
pre: " <b> 1.1. </b> "
---

## General Information

| Content         | Details                                                                                            |
| --------------- | -------------------------------------------------------------------------------------------------- |
| Duration        | 05/05/2026 - 05/10/2026                                                                            |
| Internship Week | Week 1                                                                                             |
| Phase           | Explore AWS Services                                                                               |
| Program         | First Cloud Journey                                                                                |
| Main Topics     | Account creation, cost management, IAM permissions, networking, and foundational computing         |
| Weekly Goals    | Create and secure AWS account, understand AWS Budgets, AWS Support, IAM, VPC, EC2, S3, and AWS CLI |

## Week 1 Learning Orientation

This is the first week of the internship at the **Workforce Bootcamp - First Cloud AI Journey**, following the **First Cloud Journey** roadmap in the **Explore AWS Services** phase. This week I started with the most foundational and accessible workshops: creating an AWS account, cost management, seeking support, IAM permissions, and then moved on to networking (VPC), virtual servers (EC2), and storage (S3).
Since I'm just starting out, I prioritized reading the documentation carefully and following the step-by-step guides for testing purposes, mainly to understand the core concepts rather than building a complete solution. I focused on 1-2 services per day to avoid overload.

## Week 1 Learning Objectives

- Create an AWS Account and enable basic security (MFA for the root account).
- Manage costs with AWS Budgets.
- Understand how to get help via AWS Support.
- Manage access permissions with AWS IAM (User, Group, Role, Policy).
- Explore networking infrastructure with Amazon VPC.
- Explore virtual servers with Amazon EC2 and IAM Roles for EC2.
- Perform command-line operations with AWS CLI.
- Explore static website hosting with Amazon S3.

## Activities Implemented During the Week

### Day 1 - Tuesday, 05/05/2026

Topic: **Creating Your First AWS Account** and **Managing Costs with AWS Budgets**.
Implemented Activities:

- Read the "Creating Your First AWS Account" workshop and independently created an AWS Free Tier account following the guide.
- Enabled MFA for the root account following the steps.
- Read about AWS Budgets and set up a small budget to test the email cost alert mechanism.

Achieved Results:

- Have an AWS account to use throughout the internship, with MFA enabled.
- Understand how AWS Budgets alerts when costs exceed the threshold.

### Day 2 - Wednesday, 05/06/2026

Topic: **Getting Help with AWS Support** and **Access Management with AWS IAM**.
Implemented Activities:

- Read about AWS Support plans and reviewed the process of creating a support case.
- Read IAM documentation to distinguish between User, Group, Role, and Policy.
- Learned about the least privilege principle and read a few JSON-format IAM Policies to get familiar with the structure.
- Followed the guide to create an IAM User with limited permissions instead of using the root account.

Achieved Results:

- Know where and at what level to find support when needed.
- Understand the role of each IAM component and how to create a User and assign a basic Policy.

### Day 3 - Thursday, 05/07/2026

Topic: **Networking Essentials with Amazon VPC**.
Implemented Activities:

- Read VPC documentation: CIDR block, subnet, distinguishing public and private subnets.
- Explored Route Table, Internet Gateway, NAT Gateway.
- Explored the difference between Security Group and Network ACL.
- Followed a workshop to build a VPC with public and private subnets to visualize how the components connect.

Achieved Results:

- Visualized the basic structure of a VPC.
- Distinguished between Security Group (stateful) and Network ACL (stateless), at least theoretically.

### Day 4 - Friday, 05/08/2026

Topic: **Compute Essentials with Amazon EC2**.
Implemented Activities:

- Read about EC2: AMI, instance type, key pair, EBS volume.
- Followed the guide to create a Free Tier EC2 instance in the public subnet built the previous day.
- Attempted to SSH into the instance and run a few commands to verify.

Achieved Results:

- Understood the roles of AMI, instance type, and key pair when creating virtual machines.
- Successfully connected to the newly created instance to see how it runs.

### Day 5 - Saturday, 05/09/2026

Topic: **Instance Profiling with IAM Roles for EC2** and **Command Line Operations with AWS CLI**.
Implemented Activities:

- Read about IAM Roles for EC2 (instance profile) and the reason why Access Keys shouldn't be stored directly on servers.
- Followed a tutorial to attach a Role to an EC2 instance and check permissions.
- Installed AWS CLI on the personal computer, configured Access Key, Secret Key, and Region.
- Ran a few basic commands to get familiar.

After configuring, I checked to ensure I logged into the right account:

```bash
aws sts get-caller-identity
```

```json
{
  "UserId": "AIDA********EXAMPLE",
  "Account": "123456789012",
  "Arn": "arn:aws:iam::123456789012:user/intern-dev"
}
```

At first, I forgot to run `aws configure` and executed the command right away, resulting in:

```
Unable to locate credentials. You can configure credentials by running "aws configure".
```

After running `aws configure` and re-entering the Access Key / Secret Key / Region (ap-southeast-1), it worked. Then I tried listing regions to ensure the CLI could call the API:

```bash
aws ec2 describe-regions --query "Regions[].RegionName" --output text
```

Achieved Results:

- Understood why using a Role for EC2 is safer.
- Was able to use AWS CLI for simple operations and found it faster than the Console for some tasks.
- Memorized the `aws sts get-caller-identity` command to quickly check the active account/role next time — this will likely be used a lot.

### Day 6 - Sunday, 05/10/2026

Topic: **Static Website Hosting with Amazon S3**.
Implemented Activities:

- Read about S3: bucket, object, storage class.
- Followed a workshop to create a bucket, upload a file, and enable static website hosting.
- Learned about bucket policies and the option to block public access.

I tried doing this via the CLI to get used to it. Created a bucket and uploaded the index file:

```bash
aws s3 mb s3://intern-static-demo-2026
aws s3 cp index.html s3://intern-static-demo-2026/
```

```
make_bucket: intern-static-demo-2026
upload: ./index.html to s3://intern-static-demo-2026/index.html
```

Enabled static website hosting:

```bash
aws s3 website s3://intern-static-demo-2026/ --index-document index.html
```

When opening the website endpoint for the first time, I got a `403 Forbidden`. It took a while to realize this was because Block Public Access was enabled and there was no bucket policy allowing public read access. After disabling the block at the bucket level and adding an `s3:GetObject` policy for `Principal: "*"`, the page displayed successfully.

Achieved Results:

- Created a bucket and hosted a simple static page following the guide.
- Understood how bucket policies affect whether a file is public or not.
- Memorized the `s3 mb` / `s3 cp` / `s3 website` command set so I won't have to use the Console next time.

## Week 1 Knowledge Summary

| Knowledge Group | Learned Content                                          |
| --------------- | -------------------------------------------------------- |
| Account & Cost  | AWS Account, MFA, AWS Budgets                            |
| Support         | AWS Support                                              |
| Security        | IAM User, Group, Role, Policy, least privilege           |
| Networking      | VPC, Subnet, Route Table, IGW, NAT, Security Group, NACL |
| Compute         | EC2, AMI, instance type, IAM Roles for EC2               |
| CLI             | AWS CLI                                                  |
| Storage         | S3, static website hosting, bucket policy                |

## Achievements During the Week

- Have an AWS account with MFA enabled and a cost alert budget.
- Grasped the basics of IAM, created a User, and assigned a Policy following the least privilege principle.
- Followed the workshop to set up a basic VPC and EC2 instance.
- Was able to use IAM Roles for EC2 and a few AWS CLI commands.
- Hosted a static page on S3 following the guide.

## Challenges Encountered

- The JSON-based IAM Policy initially looked quite confusing; I had to re-read it several times to get used to the Effect, Action, and Resource sections.
- Once I tried SSHing into an EC2 instance but couldn't. I struggled for a bit before realizing the inbound rules in the Security Group and the route table were incorrect.
- The S3 bucket policy part was a bit tricky. I got Access Denied a few times because I didn't fully understand how block public access worked.
- When first installing the AWS CLI, I ran commands right away and forgot `aws configure`. It reported "Unable to locate credentials," making me think the installation failed. Running the configuration fixed it.

## Lessons Learned

- I clearly see that the root account shouldn't be used for daily tasks. Creating a separate IAM User is both safer and more organized.
- Things like MFA or budgets should be enabled right from the start so they aren't forgotten and don't lead to unexpected costs.
- Reading theory isn't enough. Following workshops hands-on revealed many areas I thought I understood but actually didn't.

## Plan for Week 2

- Explore Amazon RDS (relational database).
- Explore Amazon Lightsail and Lightsail Containers.
- Explore EC2 Auto Scaling and Amazon CloudWatch.
- Explore Amazon Route 53 and AWS Cloud9.

## End of Week Review

The first week was mostly about getting familiar, reading documentation, and testing based on guides, so there wasn't anything too complex. However, this provided a foundation to make the next week easier. Starting with simpler topics before moving to VPC and EC2 helped me avoid getting overwhelmed right from the beginning.
