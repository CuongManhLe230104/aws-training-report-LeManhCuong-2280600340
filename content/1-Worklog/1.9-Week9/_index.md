---
title: "Week 9 Worklog"
date: 2026-06-15
weight: 9
chapter: false
pre: " <b> 1.9. </b> "
---

**TECHNICAL REPORT: EVALUATING SECURE NETWORK ARCHITECTURE AND CREDENTIAL MANAGEMENT ON AWS**[cite: 6]
**Name:** Lê Mạnh Cường[cite: 6]
**ID:** 2280600340[cite: 6]

### Week 9 Objectives:

* Security & Data Module: Survey the last-mile credentials protection mechanism.[cite: 6] Establish a dynamic API call flow from AWS Lambda to AWS Secrets Manager to query the Amazon RDS (MySQL) database without exposing the source code configuration.[cite: 6]
* Private Network Integration Module: Understand the operating principles and underlying technology of VPC Link on Amazon API Gateway.[cite: 6] Evaluate the architectural differences in the network system between the REST API and HTTP API models.[cite: 6]

### Tasks to be carried out this week:

| Day | Task | Start Date | Completion Date | Reference Material |
| --- | --- | --- | --- | --- |
| 1 | - Analyze credential security solutions for data systems: Survey the risks of hardcoding application passwords.[cite: 6] <br> - Establish a secure connection process to protect the backend database: Client → API Gateway → AWS Lambda → Call Secrets Manager to get configuration.[cite: 6] | 06/15/2026[cite: 6] | 06/15/2026[cite: 6] | <https://aws.amazon.com/vi/blogs/compute/understanding-vpc-links-in-amazon-api-gateway-private-integrations/>[cite: 6] |
| 2 | - Research configuration automation via CloudFormation: Learn how to use AWS CloudFormation templates to automate the initialization of resource clusters including RDS MySQL, API Gateway, and Lambda functions.[cite: 6] | 06/16/2026[cite: 6] | 06/16/2026[cite: 6] | <https://aws.amazon.com/vi/blogs/security/how-to-securely-provide-database-credentials-to-lambda-functions-by-using-aws-secrets-manager/>[cite: 6] |
| 3 | - Research Dynamic References & Automatic Rotation mechanisms: Apply Dynamic References to retrieve passwords from Secrets Manager when creating RDS, avoiding plain text logging.[cite: 6] <br> - Configure the `AWS::SecretsManager::RotationSchedule` resource in coordination with a Lambda function to automatically reset the password every 30 days.[cite: 6] | 06/17/2026[cite: 6] | 06/17/2026[cite: 6] | |
| 4 | - Distinguish the nature of Private API and Private Integration: Clearly define the system: Private API limits the endpoint of the API Gateway itself within the VPC (supported only by REST API); Private Integration protects the backend hidden in the VPC via the VPC Link connection port.[cite: 6] | 06/18/2026[cite: 6] | 06/18/2026[cite: 6] | |
| 5 | - Evaluate VPC Link infrastructure for REST API: Research the underlying technology based on AWS PrivateLink.[cite: 6] <br> - Identify constraints: Mandatory configuration via VPC Endpoint Service, connecting to a single NLB (Layer 4), and identifying the source IP from that NLB itself.[cite: 6] | 06/19/2026[cite: 6] | 06/19/2026[cite: 6] | |
| 6 | - Evaluate VPC Link infrastructure for HTTP API: Research the underlying technology based on the VPC-to-VPC NAT mechanism of the AWS Hyperplane network virtualization system.[cite: 6] <br> - Identify advantages: Direct connection via ENI "tunnels" to multiple backends (ALB, NLB, Cloud Map), leveraging the Layer 7 routing power of ALB.[cite: 6] | 06/20/2026[cite: 6] | 06/20/2026[cite: 6] | |
| 7 | - Synthesize, compare, and build an architectural report: Compare and contrast the pros and cons regarding cost and performance of the two types of VPC Links.[cite: 6] <br> - Standardize the entire system architecture diagram and package the weekly progress report document.[cite: 6] | 06/21/2026[cite: 6] | 06/21/2026[cite: 6] | |

### Week 9 Achievements:

* Successfully analyzed and established a secure connection process to protect backend databases, eliminating the risk of hardcoded passwords.[cite: 6]
* Successfully researched infrastructure configuration automation (RDS, API Gateway, Lambda) via AWS CloudFormation.[cite: 6]
* Successfully applied the Dynamic References mechanism and automatic password rotation (RotationSchedule) every 30 days via Secrets Manager.[cite: 6]
  ![AWS Secrets Manager Database Rotation](images/week9_secretsmanager.png)
* Clearly distinguished and defined the architectural nature between Private API and Private Integration.[cite: 6]
* Completed the evaluation of VPC Link infrastructure for both REST API (based on AWS PrivateLink) and HTTP API (based on AWS Hyperplane).[cite: 6]
  * **REST API VPC Link Architecture:**
    ![REST API VPC Link Architecture](images/week9_vpclink_rest.png)
  * **HTTP API VPC Link (NLB) Architecture:**
    ![HTTP API VPC Link NLB Architecture](images/week9_vpclink_http_nlb.png)
  * **HTTP API VPC Link (Hyperplane/ALB) Architecture:**
    ![HTTP API VPC Link Hyperplane ALB Architecture](images/week9_vpclink_http_alb.png)
* Built a comprehensive architectural report detailing the pros and cons of different VPC Link types.[cite: 6]