---
title: "Proposal"
date: 2024-01-01
weight: 2
chapter: false
pre: " <b> 2. </b> "
---

In this section, you need to summarize the contents of the workshop that you **plan** to conduct.

# SmartMenu – AI-Powered Smart Electronic Menu System on AWS Serverless Platform

### 1. Executive Summary

SmartMenu is an electronic menu system designed for restaurants and diners, built on the AWS cloud computing platform using the Serverless model. The system allows customers to access menus online via mobile devices, view dish information, receive language translation support and AI-powered food recommendations, and quickly place orders.
Additionally, SmartMenu provides an administrative interface to help restaurant owners manage the menu, track orders, and update data in real time. Applying a Serverless architecture makes the system flexibly scalable, reduces operating costs, and eliminates server management requirements.

### 2. Objectives

**General Objective:**
Build an intelligent electronic menu system on AWS to enhance customer experience and support restaurants in managing more effectively.

**Specific Objectives:**

- Build an electronic menu system operating on the AWS Serverless platform.
- Support online menu viewing and ordering.
- Support menu translation into multiple languages.
- AI-powered food recommendation and consulting.
- Manage menus and orders in real-time.
- Optimize operational costs.
- Ensure scalability and high availability.

### 3. Problem Statement

Currently, many restaurants still use paper menus and traditional service processes, leading to the following issues:

- Customers have to wait for staff to order.
- Hard to update the menu when prices change or new dishes are added.
- High costs for printing paper menus.
- International customers face language barriers.
- Customers with food allergies find it hard to get detailed information about ingredients.
- Restaurant owners struggle to manage orders during peak hours.
- Traditional systems are difficult to scale as customer volume grows.

Therefore, it is necessary to build a system that digitalizes the entire menu viewing and ordering process.

### 4. Solution Architecture

**Technologies Used:**

- **Frontend Web:** ReactJS + Vite, building interfaces for customers (Table Menu Client) and administrators (Manager Client).
- **Backend:** AWS Lambda (Node.js), deployed under the Serverless model to handle system business logic.
- **AI:** Amazon Bedrock, supporting multi-language translation and dish recommendations.
- **Database:** Amazon DynamoDB, storing menu and order data.

**Key AWS Services:**

- **Amazon API Gateway:** Receives and routes requests from applications to backend services.
- **AWS Lambda:** Processes business logic such as menu management, ordering, and language translation.
- **Amazon DynamoDB:** Stores menu data, orders, and system information.
- **Amazon S3:** Hosts the web interface and static assets like images, CSS, and JavaScript.
- **Amazon CloudFront:** Distributes content from Amazon S3 with low latency and accelerates access speed.
- **Amazon Bedrock:** Provides AI models for translation and dish recommendation functions.
- **AWS IAM:** Manages users, roles, and permissions access between AWS services.
- **AWS WAF:** Protects the system from common web exploits.
- **Amazon CloudWatch:** Monitors the system, collects logs, metrics, and sends alerts when issues occur.

![SmartMenu Architecture](/images/2-Proposal/smartmenu_architecture.png)

### 5. Technical Implementation

#### 5.1. Implementation Phases

- **Phase 1:** Learn fundamental AWS services through CloudJourney Labs, including IAM, VPC, EC2, RDS, S3, Lambda, API Gateway, CloudFormation, and DynamoDB.
- **Phase 2:** Analyze SmartMenu system requirements, design Serverless architecture, build a Solution Architecture diagram, and set up the development environment.
- **Phase 3:** Develop core features of the system, including customer and admin interfaces, services for menu management, order management, translation, and AI integration.
- **Phase 4:** Deploy the system to AWS, conduct testing, optimize performance, monitor the system, and complete project documentation.

#### 5.2. Technical Requirements

**Technology Stack:**

- **Frontend:** ReactJS, Vite, HTML5, CSS3, JavaScript.
- **Backend:** AWS Lambda (Node.js).
- **Database:** Amazon DynamoDB.
- **AI Services:** Amazon Bedrock.
- **API:** Amazon API Gateway (REST API).

**AWS Infrastructure Requirements:**

- Amazon S3 and CloudFront for web interface deployment.
- AWS Lambda for backend business logic.
- Amazon API Gateway to expose REST APIs.
- Amazon DynamoDB for data storage.
- AWS IAM and AWS WAF for system security.
- Amazon CloudWatch for monitoring and logging.

**Non-Functional Requirements:**

- The system automatically scales based on the number of concurrent users.
- API response times under 2 seconds under normal operating conditions.
- Data is backed up and recoverable in case of failures.
- Secure authentication and proper authorization mechanisms are enforced.

### 6. Timeline & Milestones

#### Phase 1: Study and Learn AWS Platform

_Timeline: 20/04/2026 – 15/05/2026 (Week 1 – Week 4)_

- **Week 1 (20/04 – 24/04):**
  - Learn overview of Cloud Computing and Amazon Web Services (AWS).
  - Get familiar with AWS Management Console and AWS CLI.
- **Week 2 (27/04 – 01/05):**
  - Practical labs on: AWS IAM, Amazon VPC, Amazon EC2, Amazon RDS.
- **Week 3 (04/05 – 08/05):**
  - Practical labs on: Amazon S3, AWS Lambda, Amazon API Gateway.
- **Week 4 (11/05 – 15/05):**
  - Practical labs on: AWS CloudFormation, Amazon DynamoDB.
  - Learn AWS Well-Architected Framework and Serverless architecture on AWS.

#### Phase 2: Analyze, Design, and Develop SmartMenu System

_Timeline: 18/05/2026 – 12/06/2026 (Week 5 – Week 8)_

- **Week 5 (18/05 – 22/05):**
  - Learn business requirements of the SmartMenu system.
  - Analyze problems and define core functions.
  - Set up the development environment.
- **Week 6 (25/05 – 29/05):**
  - Design AWS architecture for the system.
  - Build the AWS Solution Architecture diagram.
  - Design database schemas on DynamoDB.
- **Week 7 (01/06 – 05/06):**
  - Develop Table Menu Client and Manager Client UI.
  - Build Menu Service and Order Service.
- **Week 8 (08/06 – 12/06):**
  - Develop Translation Service.
  - Integrate Amazon Bedrock for translation and AI advice.
  - Connect backend services with DynamoDB.

#### Phase 3: Deploy, Test, and Finalize System

_Timeline: 15/06/2026 – 10/07/2026 (Week 9 – Week 12)_

- **Week 9 (15/06 – 19/06):**
  - Deploy frontend to Amazon S3 and Amazon CloudFront.
  - Deploy APIs using Amazon API Gateway and AWS Lambda.
  - Configure IAM and integrate AWS services.
- **Week 10 (22/06 – 26/06):**
  - Perform Unit Tests and Integration Tests.
  - Load test and optimize Lambda, DynamoDB.
- **Week 11 (29/06 – 03/07):**
  - Optimize UI and User Experience.
  - Optimize operational cost on AWS.
  - Write technical and architecture documentation.
- **Week 12 (06/07 – 10/07):**
  - End-to-end testing.
  - Bug fixes and final release.

### 7. Budget Estimation

System operational costs are estimated using the AWS Pricing Calculator, assuming the system serves about 100–200 customers daily, equivalent to 5,000 requests and 2,000–3,000 orders monthly.

#### Infrastructure Costs

| AWS Service              | Assumed Configuration        | Monthly Cost (USD) | Monthly Cost (VND) |
| ------------------------ | ---------------------------- | ------------------ | ------------------ |
| **AWS Lambda**           | 5,000 requests, 512 MB RAM   | $0.02              | ~500 VND           |
| **Amazon API Gateway**   | 5,000 API requests           | $0.02              | ~500 VND           |
| **Amazon DynamoDB**      | Storing menu and orders      | $2.50              | ~65,000 VND        |
| **Amazon S3 Standard**   | 5 GB storage                 | $0.20              | ~5,200 VND         |
| **Amazon CloudFront**    | 10 GB data transfer          | $1.50              | ~39,000 VND        |
| **Amazon Bedrock**       | Translation and AI advisor   | $8.00              | ~208,000 VND       |
| **Amazon CloudWatch**    | Monitoring and logging       | $0.50              | ~13,000 VND        |
| **AWS IAM**              | User management and policies | Free               | 0 VND              |
| **Total Estimated Cost** |                              | **~$12.74**        | **~331,000 VND**   |

- **Cost for 12 months:** 12.74 × 12 = $152.88/year (equivalent to approximately **3,975,000 VND/year**).

#### Hardware Costs

Since the SmartMenu system is fully deployed on the AWS cloud platform under a Serverless architecture, there is no need to invest in physical servers or proprietary hardware.

- **Hardware Costs:** 0 VND

### 8. Risk Assessment

#### Main Risks

- **System Overload:** Sudden spike in traffic can increase API Gateway and Lambda requests.
- **Data Loss:** Application bugs or manual errors can affect menu and order data in DynamoDB.
- **DDoS/Bot Attacks:** Malicious traffic could degrade performance and inflate running costs.
- **AWS Budget Overrun:** Costs might escalate if request counts to Lambda, API Gateway, or Amazon Bedrock grow significantly.

#### Mitigation Strategies

- Use Serverless architecture to automatically scale resources.
- Enable Point-in-Time Recovery (PITR) for DynamoDB and perform scheduled backups.
- Utilize AWS WAF, Rate Limiting, and IAM Least Privilege principles to improve security.
- Set up AWS Budgets and CloudWatch Billing Alarms to monitor and control spending.

#### Contingency Plans

- Recover data from DynamoDB or backups on Amazon S3 when issues occur.
- In case Amazon Bedrock is unavailable, the system will keep basic functions like viewing menus and placing orders active while temporarily disabling AI-powered features.

### 9. Expected Outcomes

#### Technical Improvements

- Successfully build the SmartMenu system on AWS Serverless architecture.
- Deploy core functions: menu viewing, ordering, menu management, and AI food consulting.
- Ensure high availability, scalability, and low operational costs.
- Apply AWS services (API Gateway, Lambda, DynamoDB, S3, CloudFront, Bedrock) to a real-world project.

#### Long-Term Value

- Help restaurants digitize ordering, reducing wait times and operating costs.
- Enhance guest experience with multi-language translation and AI assistance.
- Establish a scalable foundation for future features (e.g., online payment, data analytics, multi-branch management).
- Gain hands-on experience in design, deployment, and operation on AWS Cloud.
- Potential to develop into a commercial product in the future.
