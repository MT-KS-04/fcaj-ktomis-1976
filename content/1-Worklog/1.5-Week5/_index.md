---
title: "Week 5 Worklog"
date: 2026-06-01
weight: 5
chapter: false
pre: " <b> 5.1. </b> "
---

### Week 5 Goals:

- Learn Infrastructure as Code with AWS CloudFormation and AWS CDK.
- Understand how to manage service limits with Service Quotas.
- Know how to track, analyze costs, and optimize resources on AWS.

### Activities Implemented During the Week:

| Day | Activities                                                                                                                                                                                                                                                                                                    | Start Date | Completion Date | Reference                          |
| --- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------- | --------------- | ---------------------------------- |
| 2   | - Explored Infrastructure as Code (IaC) <br> - Explored AWS CloudFormation: <br>&emsp; + Template structure (Resources, Parameters, Outputs) <br>&emsp; + Stack and Change set <br> - **Hands-on:** <br>&emsp; + Wrote and deployed a template to create resources <br>&emsp; + Checked the stack's resources | 01/06/2026 | 01/06/2026      | <https://000037.awsstudygroup.com> |
| 3   | - Explored AWS CDK: <br>&emsp; + Construct, Stack, App <br>&emsp; + Compared CDK with plain CloudFormation <br> - **Hands-on:** <br>&emsp; + Initialized a CDK project <br>&emsp; + Ran `cdk synth` and `cdk bootstrap` <br>&emsp; + Deployed a stack with CDK                                                | 02/06/2026 | 02/06/2026      | <https://000038.awsstudygroup.com> |
| 4   | - Explored Service Quotas: <br>&emsp; + The meaning of service limits <br>&emsp; + How to view current quotas <br>&emsp; + The process for requesting a quota increase <br> - **Hands-on:** <br>&emsp; + Checked the quota of a few services                                                                  | 03/06/2026 | 03/06/2026      | <https://000063.awsstudygroup.com> |
| 5   | - Explored Cost and Usage Management: <br>&emsp; + Cost Explorer <br>&emsp; + Cost and Usage Report (CUR) <br>&emsp; + Cost allocation by tag <br> - **Hands-on:** <br>&emsp; + Analyzed cost trends in Cost Explorer                                                                                         | 04/06/2026 | 04/06/2026      | <https://000064.awsstudygroup.com> |
| 6   | - Explored EC2 Resource Optimization: <br>&emsp; + The right-sizing concept <br>&emsp; + Choosing instance types based on metrics <br>&emsp; + Tools providing optimization recommendations <br> - **Hands-on:** <br>&emsp; + Evaluated an instance's sizing                                                  | 05/06/2026 | 05/06/2026      | <https://000032.awsstudygroup.com> |
| 7   | - Explored VPC Flow Logs: <br>&emsp; + The structure of a flow log record <br>&emsp; + Pushing logs to CloudWatch Logs or S3 <br> - **Hands-on:** <br>&emsp; + Enabled flow logs and analyzed records <br>&emsp; + Filtered by ACCEPT/REJECT <br> - Summarized Week 5 knowledge                               | 06/06/2026 | 06/06/2026      | <https://000074.awsstudygroup.com> |

### Achievements During Week 5:

- Understood and applied Infrastructure as Code with AWS CloudFormation:
  - The structure of a template: Resources, Parameters, Outputs
  - The concepts of stack and change set
  - Deployed infrastructure from a template instead of manual clicks in the Console
  - Learned that YAML is sensitive to indentation and needs careful writing

- Learned AWS CDK and how to write infrastructure using a programming language:
  - The concepts of construct, stack, app
  - The lifecycle: init → synth → bootstrap → deploy
  - Understood that a new account must run `cdk bootstrap` once before deploying
  - Compared the advantages of CDK over writing plain YAML

- Understood the role of Service Quotas in operations:
  - The impact of quotas on system scalability
  - How to check and request a quota increase when needed

- Learned how to track and manage costs on AWS:
  - Analyzed cost trends with Cost Explorer
  - Understood the Cost and Usage Report
  - Used tags for cost allocation by group

- Learned resource optimization with right-sizing:
  - Choosing instance types based on metrics instead of guesswork
  - Balancing cost and performance

- Monitored networking with VPC Flow Logs:
  - Read and understood the structure of a flow log record
  - Filtered by ACCEPT/REJECT to diagnose connections and check security
