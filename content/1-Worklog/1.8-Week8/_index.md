---
title: "Week 8 Worklog"
date: 2026-06-08
weight: 8
chapter: false
pre: " <b> 1.8. </b> "
---

**Developing Extended APIs & Authorization for SaaS HR Multi-tenant System**
**Name:** Lê Mạnh Cường
**ID:** 2280600340

### Week 8 Objectives:

* Cloud-Native & Zero-Trust Architecture: Deploy the entire network, security, and storage infrastructure for the SaaS HR project entirely using manual Terraform source code, ensuring no connections are accepted unless explicitly authorized.
* Extreme Cost Optimization (FinOps): Squeeze operating costs from standard levels down to approximately $70 - $95/month, maintaining below the budget ceiling of $120 - $150/month.
* Identity & Security Management: Manage group access through IAM Identity Center (MFA required) and manage application users via AWS Cognito.

### Tasks to be carried out this week:

| Day | Task | Start Date | Completion Date | Reference Material |
| --- | --- | --- | --- | --- |
| 1 | - Lock the root account and configure IAM Identity Center with mandatory MFA. <br> - Initialize AWS Budgets with a $100 alert threshold. <br> - Set up CloudTrail and Terraform remote state on S3. | 06/08/2026 | 06/08/2026 | |
| 2 | - Build a single VPC containing Public and Private Subnets spread across two AZs (ap-southeast-1a and 1b). <br> - Design a network model that completely eliminates the NAT Gateway to save $32.85/month. | 06/09/2026 | 06/09/2026 | |
| 3 | - Launch RDS MySQL 8.0 (db.t4g.micro) running 24/7 in the Private Subnet. <br> - Store sensitive information as static SecureStrings in the SSM Parameter Store completely free of charge. <br> - Consolidate three databases (auth, tenant, hr) into a single instance to optimize resources. | 06/10/2026 | 06/10/2026 | |
| 4 | - Push three microservices source code directories to Amazon ECR. <br> - Launch four tasks (including Redis) on ECS Fargate Spot, helping to reduce server costs by 70%. <br> - Configure an Application Load Balancer (ALB) to route paths to the APIs. | 06/11/2026 | 06/11/2026 | |
| 5 | - Configure a WAF v2 Web ACL in the us-east-1 region to attach to CloudFront. <br> - Apply core protection rule sets, SQLi prevention, and request limits. | 06/12/2026 | 06/12/2026 | |
| 6 | - Migrate the Authentication flow to Cognito User Pools. <br> - Retain the internal database for Authorization purposes and tenant management. | 06/13/2026 | 06/13/2026 | |
| 7 | - Initialize an S3 Bucket that blocks public access, only allowing Origin Access Control (OAC) from CloudFront. <br> - Register a domain name via Route 53 and point an ALIAS to CloudFront. | 06/14/2026 | 06/14/2026 | |

### Architecture Components Summary

![SaaS HR Multi-Tenant AWS Architecture](images/architecture.png)

| Tier / Zone | AWS Service | Role | Network Location |
| --- | --- | --- | --- |
| DNS (Global Edge) | Amazon Route 53 | Domain name resolution → CloudFront | Global (Edge) |
| CDN & Security (Edge) | Amazon CloudFront + AWS WAF | Edge caching, DDoS protection, Web ACL filtering (WAF managed in us-east-1) | Global (Edge) |
| Static Hosting (Region) | Amazon S3 | Serve React frontend build (Private access via Origin Access Control - OAC) | Regional (ap-southeast-1) |
| Authentication (Region) | AWS Cognito (User Pools) | Manage user authentication, issue JWT tokens (custom attribute: custom:tenant_id) | Regional (ap-southeast-1) |
| Key Management (Region) | AWS SSM Parameter Store | Store encrypted secret configurations as SecureStrings (Static & Free) | Regional (ap-southeast-1) |
| Load Balancing (VPC) | Application Load Balancer (ALB) | Route based on `/api/v1/*` paths to ECS target groups | Public Subnet (ap-southeast-1a / 1b) |
| Compute (VPC) | Amazon ECS Fargate Spot (4 Tasks) | Auth, Tenant, HR microservices + Redis (Pub/Sub broker) connected via AWS Cloud Map | Public Subnet (ap-southeast-1a / 1b) |
| SIEM/SOC Monitoring (VPC)| EC2 t3.small Spot (Wazuh Manager) | Security monitoring center & centralized log analysis (Same VPC, private subnet) | Public Subnet SOC (ap-southeast-1a, 10.0.3.0/24) |
| Database (VPC) | Amazon RDS MySQL (db.t4g.micro) | 1 instance containing 3 databases: auth_db, tenant_db, hr_db | Private Subnet (ap-southeast-1a / 1b) |
| Administration (Account)| AWS IAM Identity Center + CloudTrail + AWS Budgets | Manage SSO, audit system activities, and budget alerts ($100 alert) | Account Level |

### FinOps & Cost Optimization Summary

| AWS Service | Detailed Configuration | Standard Cost (24/7) | Optimized Cost | Optimization Strategy |
| --- | --- | --- | --- | --- |
| AWS WAF | 1 Web ACL, 3 Managed Rules (Core, SQLi, IP Rep) | $8.60 | $8.60 | Attach to CloudFront to protect the edge and ALB. |
| CloudFront & S3 | 100 GB Data Transfer Out, S3 Storage (React App) | $9.50 | $0.50 | S3 Static Hosting, CloudFront Free Tier (1TB free/month). |
| AWS ALB | 1 Load Balancer, 1 LCU | $22.27 | $22.27 | Essential for path-based target groups routing. |
| ECS Fargate | 4 Tasks (0.25 vCPU, 0.5 GB RAM per task) | $32.40 | $9.72 | Fargate Spot (save 70% compared to On-Demand). |
| RDS MySQL | 1 Instance db.t4g.micro (2 vCPU, 1GB RAM) + 20GB gp3 | $13.98 | $5.70 | Auto-stop schedule (run 10h/day, Mon - Fri). |
| EC2 (Wazuh) | 1 Instance t3.small (2 vCPU, 2GB RAM) + 30GB gp3 | $17.58 | $6.20 | EC2 Spot Instance + Auto-stop outside test hours. |
| AWS Cognito & SSM | Cognito User Pools + SSM Parameter Store | $0.00 | $0.00 | Free Tier supports up to 50,000 MAUs and free parameter storage. |
| NAT Gateway | 1 NAT Gateway (Standard VPC requirement) | $32.85 | $0.00 | VPC design without NAT (ECS runs in public subnets). |
| Data Transfer/CloudWatch| Logs, Inter-AZ bandwidth | $10.00 | $3.00 | Rotate logs & retain for a maximum of 7 days. |
| **Total / Month** | | **$147.18** | **$56.99** | **Total savings: ~61% ($90.19 saved/month)** |

### Week 8 Achievements:

* Established a solid security foundation with IAM Identity Center, CloudTrail, and AWS Budgets ($100 alert).
* Successfully built a VPC eliminating the NAT Gateway, configuring cost-optimized Public/Private Subnets.
* Operated RDS MySQL with resource optimization (consolidating 3 databases) and secured parameters with SSM Parameter Store.
* Successfully deployed ECS Fargate Spot and ALB, leading to significant server cost savings.
* Implemented excellent edge security through AWS WAF, CloudFront, and integrated AWS Cognito for the authentication flow.
* Perfected the FinOps strategy with an estimated total savings of 61% (reducing costs from $147.18 to $56.99/month).