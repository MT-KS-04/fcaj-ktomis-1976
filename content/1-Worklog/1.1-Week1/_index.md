---
title: "Week 1 Worklog"
date: 2026-05-05
weight: 1
chapter: false
pre: " <b> 1.1. </b> "
---

### Week 1 Goals:

- Get acquainted and connect with fellow members of the First Cloud AI Journey.
- Create and secure an AWS account, and understand how to manage costs.
- Understand core AWS services: IAM, VPC, EC2, S3, and how to use the Console & CLI.

### Activities Implemented During the Week:

| Day | Activities                                                                                                                                                                                                                                                                                                                                                                | Start Date | Completion Date | Reference                                                                                                          |
| --- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------- | --------------- | ------------------------------------------------------------------------------------------------------------------ |
| 3   | - Got acquainted with FCAJ members <br> - Read and noted the rules and regulations at the internship unit <br> - Reviewed an overview of the First Cloud Journey learning roadmap                                                                                                                                                                                         | 05/05/2026 | 05/05/2026      | <https://cloudjourney.awsstudygroup.com/1-explore/>                                                                |
| 4   | - Explored cloud computing and AWS service groups <br>&emsp; + Compute <br>&emsp; + Storage <br>&emsp; + Networking <br>&emsp; + Database <br>&emsp; + ... <br> - **Hands-on:** <br>&emsp; + Created an AWS Free Tier account <br>&emsp; + Enabled MFA for the root account <br>&emsp; + Set up AWS Budgets cost alerts                                                   | 06/05/2026 | 06/05/2026      | <https://000001.awsstudygroup.com> <br> <https://000007.awsstudygroup.com>                                         |
| 5   | - Explored AWS Support and how to create a support case <br> - Explored AWS IAM: <br>&emsp; + User, Group <br>&emsp; + Role, Policy <br>&emsp; + Least privilege principle <br> - **Hands-on:** <br>&emsp; + Created an IAM User with limited permissions <br>&emsp; + Read the JSON structure of an IAM Policy                                                           | 07/05/2026 | 07/05/2026      | <https://000009.awsstudygroup.com> <br> <https://000002.awsstudygroup.com>                                         |
| 6   | - Explored Amazon VPC: <br>&emsp; + CIDR block, Subnet <br>&emsp; + Route Table, Internet Gateway, NAT Gateway <br>&emsp; + Security Group vs Network ACL <br> - **Hands-on:** <br>&emsp; + Built a VPC with public and private subnets                                                                                                                                   | 08/05/2026 | 08/05/2026      | <https://000003.awsstudygroup.com>                                                                                 |
| 7   | - Explored Amazon EC2: <br>&emsp; + Instance types, AMI <br>&emsp; + Key pair, EBS volume <br> - Explored IAM Roles for EC2 (instance profile) <br> - **Hands-on:** <br>&emsp; + Launched a Free Tier EC2 instance <br>&emsp; + Connected via SSH to the instance <br>&emsp; + Installed & configured AWS CLI <br>&emsp; + Used the `aws sts get-caller-identity` command | 09/05/2026 | 09/05/2026      | <https://000004.awsstudygroup.com> <br> <https://000048.awsstudygroup.com> <br> <https://000011.awsstudygroup.com> |
| Sun | - Explored Amazon S3: <br>&emsp; + Bucket, Object, Storage class <br>&emsp; + Bucket policy, Block Public Access <br> - **Hands-on:** <br>&emsp; + Created a bucket and uploaded a file <br>&emsp; + Enabled static website hosting <br>&emsp; + Configured a bucket policy for public access                                                                             | 10/05/2026 | 10/05/2026      | <https://000057.awsstudygroup.com>                                                                                 |

### Achievements During Week 1:

- Understood what cloud computing is and grasped the basic AWS service groups:
  - Compute
  - Storage
  - Networking
  - Database

- Successfully created and secured an AWS Free Tier account:
  - Enabled MFA for the root account
  - Set up AWS Budgets with email alerts

- Learned AWS IAM and how to control access permissions:
  - Distinguished between User, Group, Role, Policy
  - Created a dedicated IAM User instead of using the root account
  - Applied the least privilege principle
  - Understood the Policy structure (Effect, Action, Resource)

- Understood and built basic network infrastructure with Amazon VPC:
  - Split resources across public subnet and private subnet
  - Configured Route Table and Internet Gateway
  - Distinguished Security Group (stateful) from Network ACL (stateless)

- Launched and connected to an Amazon EC2 virtual server:
  - Chose an appropriate AMI and instance type
  - Connected via SSH using a key pair
  - Attached an IAM Role to EC2 instead of storing an Access Key on the server

- Installed and configured AWS CLI on the computer, including:
  - Access Key
  - Secret Key
  - Default Region

- Used AWS CLI to perform basic operations such as:
  - Checking the currently active account
  - Listing available regions
  - Creating a bucket and uploading a file to S3
  - Enabling static website hosting

- Successfully hosted a static website on Amazon S3 and understood how bucket policy affects public access.
- Gained the ability to work in parallel between the web interface (Console) and the command line (CLI) to manage AWS resources.
