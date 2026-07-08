---
title: "Proposal"
date: 2026-06-27
weight: 2
chapter: false
pre: " <b> 2. </b> "
---

# SaaS HR Multi-Tenant Platform on AWS
## A Secure, Scalable, and Cost-Optimized Cloud-Native HR Management Solution

### 1. Executive Summary
The SaaS HR Multi-Tenant platform is a cloud-native HR management solution designed for Small and Medium Enterprises (SMEs). The platform enforces strict tenant data isolation, ensuring that each subscribing company's employee, department, and payroll data is segregated and protected using a zero-trust model. Built using FastAPI microservices and React, the system leverages AWS managed services—including ECS Fargate, ALB, RDS MySQL Multi-AZ, S3, CloudFront, Cognito, SQS, Secrets Manager, and CloudWatch—to deliver high availability, automated scaling, and cost efficiency.

---

### 2. Problem Statement

#### What's the Problem?
SMEs require reliable HR management software but often lack the capital and technical expertise to deploy and maintain dedicated servers. Traditional single-tenant deployments are costly and hard to scale, while basic multi-tenant setups frequently suffer from weak security boundaries and data leakage risks.

#### The Solution
The proposed solution is a fully managed, multi-tenant HR SaaS on AWS. The application separates tenant data at the API layer by extracting `tenant_id` claims from secure RS256 JWT tokens. The infrastructure is serverless and highly available, utilizing ECS Fargate for compute and RDS MySQL Multi-AZ for relational database storage. 

#### Benefits and Return on Investment (ROI)
- **Zero Maintenance Overhead:** Serverless tasks (Fargate) eliminate the need to patch or manage virtual machines.
- **Strict Data Isolation:** Protects client compliance by isolating data at the application and network layers.
- **Significant Cost Savings:** Implementing FinOps strategies (NAT Gateway removal, RDS scheduling, ECS Spot tasks) reduces monthly costs by 61% from $132.80 USD to $51.70 USD.
- **Fast Break-Even:** Achieved within 3-6 months due to reduced operational labor and optimized cloud spending.

---

### 3. Solution Architecture

The platform employs a secure, multi-tier AWS architecture spanning two Availability Zones (AZs) for high availability:

![SaaS HR Multi-Tenant Architecture](/images/5-Workshop/5.1-Overview/architecture.png)

#### AWS Services Used
- **Amazon CloudFront**: Acts as the global content delivery network (CDN) and secure entry point.
- **Amazon S3**: Hosts the React static frontend with all public access blocked via Origin Access Control (OAC).
- **Amazon Cognito**: Manages user authentication and authorization token generation.
- **Application Load Balancer (ALB)**: Performs path-routing (`/api/v1/*`) to backend target groups.
- **Amazon ECS (Fargate)**: Runs FastAPI microservices (`auth`, `tenant`, and `hr`) as serverless containers.
- **Amazon RDS (MySQL)**: Provides managed, relational database storage configured in Multi-AZ for auto-failover.
- **Amazon SQS**: Handles asynchronous event message decoupling between microservices.
- **AWS Secrets Manager**: Manages database credentials securely with automated Lambda-based rotation.
- **Amazon CloudWatch & SNS**: Aggregates container logs and triggers metric alarms (CPU/Memory thresholds).

#### Component Design
- **Presentation Tier:** Users access the system via CloudFront. Static assets are securely fetched from S3.
- **Application Tier:** FastAPI microservices run on ECS Fargate inside private subnets, exposed only to the ALB.
- **Data Tier:** The RDS database is isolated in private DB subnet groups, accepting traffic only from ECS tasks.
- **Messaging Integration:** SQS queues decouple high-latency tasks (e.g. tenant synchronization) to optimize API response times.

---

### 4. Technical Implementation

#### Implementation Phases
- **Phase 1: Architecture Design & Cost Calculation (Weeks 1-2):** Map microservices dependencies and estimate base running costs using the AWS Pricing Calculator.
- **Phase 2: Networking & Security Baseline (Weeks 3-5):** Build the secure multi-subnet VPC, configure Security Groups, and set up RDS Multi-AZ.
- **Phase 3: Microservices Deployment & Routing (Weeks 6-8):** Dockerize the services, push to ECR, and configure ALB path-based routing rules.
- **Phase 4: Frontend Hosting & Secrets Management (Weeks 9-10):** Set up CloudFront OAC, deploy the React build to S3, and configure AWS Secrets Manager password rotation.
- **Phase 5: Observability & Cost Optimization (Weeks 11-12):** Configure CloudWatch CPU utilization alarms, schedule RDS off-hours shutdowns, and transition tasks to ECS Spot.

#### Technical Requirements
- Containerized microservices using Docker.
- Terraform configuration files for Infrastructure as Code (IaC) automation.
- Python Lambda scripts configured for Secrets Manager rotation schedule (every 30 days).

---

### 5. Timeline & Milestones

- **Milestone 1 (End of Month 1):** Networking, Active Directory, and database infrastructures fully operational on AWS.
- **Milestone 2 (End of Month 2):** Microservices dockerized, API Gateway configured, and serverless compute tier deployed.
- **Milestone 3 (End of Month 3):** React frontend integrated via CDN, automated database rotation configured, FinOps cost optimizations applied, and end-to-end validation completed.

---

### 6. Budget Estimation

You can find the budget estimation on the [AWS Pricing Calculator](https://calculator.aws/#/estimate?id=621f38b12a1ef026842ba2ddfe46ff936ed4ab01).

#### Monthly Infrastructure Costs (FinOps Optimized)
- **ECS Fargate Compute (Spot):** $18.40/month
- **Amazon RDS MySQL (db.t4g.micro Multi-AZ):** $22.50/month
- **Application Load Balancer & Data Transfer:** $8.30/month
- **CloudFront, S3 & SSM/Cognito:** $2.50/month
- **Total Monthly Budget:** **$51.70 USD** (Saved 61% compared to baseline $132.80 USD cost).

---

### 7. Risk Assessment

#### Risk Matrix
- **Data Access Cross-contamination:** High impact, low probability. Mitigation: Enforce strict token parsing to validate the `tenant_id` claim in every request.
- **Secrets Exposure:** High impact, low probability. Mitigation: Zero hardcoded credentials; retrieve database passwords dynamically from AWS Secrets Manager.
- **Budget Overruns:** Medium impact, low probability. Mitigation: Configure AWS Billing Budgets and CloudWatch metric alarms.

---

### 8. Expected Outcomes

- **Enterprise SaaS Readiness:** A secure, scalable, and isolated multi-tenant HR management application.
- **Zero-Trust Security Alignment:** Private subnets deployment, WAF web traffic filtering, and automated credentials rotation.
- **Maximized Cost Efficiency:** Highly optimized resource allocation reducing monthly hosting fees to a minimum.