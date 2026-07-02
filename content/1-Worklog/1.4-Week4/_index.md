---
title: "Week 4 Worklog"
date: 2026-05-11
weight: 4
chapter: false
pre: " <b> 1.4. </b> "
---

**Name:** Lê Mạnh Cường
**ID:** 2280600340

### Week 4 Objectives:

* Infrastructure: Initialize and configure network environments (VPC, Security Group) for different types of operating systems.
* Administration: Master virtual server (EC2) operations such as configuration changes, backups (Snapshot), and packaging (AMI).
* Security & Recovery: Practice alternative access methods when credentials (Key Pair) are lost.
* Deployment: Install a Web Server environment (LAMP/XAMPP) and deploy a real-world Node.js application.
* Amazon RDS Administration: Understand Relational Database services, how to configure security, backups, and high availability (Multi-AZ).
* Storage with Amazon S3 (Module 6): Understand Object Storage, access management, and advanced features such as Static Website Hosting and Versioning.

### Tasks to be carried out this week:

| Day | Task | Start Date | Completion Date | Reference Material |
| --- | --- | --- | --- | --- |
| 1 | - Perform preparation steps. <br> - Deploy Microsoft AD on AWS. <br> - Establish a secure connection to RDGW. <br> - Configure the internal Domain Name System (Setup DNS). | 05/11/2026 | 05/11/2026 | <https://000004.awsstudygroup.com/> |
| 2-3 | - Check Prerequisites & Configure Network ACLs. <br> - Initialize VPC Peering connections between networks. <br> - Update Route Tables for Subnets. <br> - Set up Cross-Peer DNS to resolve services via hostname. <br> - Apply IAM Policies to limit permissions by Region and Instance Type. <br> - Deploy a Node.js CRUD application on the LAMP/XAMPP platform. | 05/12/2026 | 05/13/2026 | <https://000004.awsstudygroup.com/> |
| 4-5 | - Prepare RDS infrastructure: Create VPC, EC2 Security Group, RDS Security Group, and DB Subnet Group. <br> - Initialize RDS: Create database instances (MySQL/MariaDB/PostgreSQL). <br> - Deploy an application to connect to the RDS Database. <br> - Practice Backup & Restore: Create DB Snapshots and restore data. <br> - Learn about Multi-AZ (High Availability) and Read Replicas (Scalability). | 05/14/2026 | 05/15/2026 | <https://000005.awsstudygroup.com/> |
| 6-7 | - Create an S3 Bucket, practice Uploading/Downloading objects. <br> - Configure Bucket Policies and ACLs to manage access. <br> - Enable Versioning and Static Website Hosting. <br> - Learn about Storage Classes to optimize costs. <br> - Test data flow: App (EC2) -> DB (RDS) -> Media (S3). | 05/16/2026 | 05/17/2026 | <https://000006.awsstudygroup.com/> |

### Week 4 Achievements:

* **Module 4 (Network, Compute & LAMP):** Finalized VPC Peering environments, set up Cross-Peer DNS, applied IAM Policies limiting permissions by Region/Instance Type, and successfully deployed a Node.js CRUD app on a LAMP/XAMPP platform.
* **Module 5 (Amazon RDS):** Prepared infrastructure and successfully initialized RDS instances (MySQL/MariaDB/PostgreSQL); practiced Backup & Restore (DB Snapshots) and grasped Multi-AZ and Read Replica mechanisms.
* **Module 6 (Amazon S3):** Managed object storage with S3 Buckets, configured secure Bucket Policies/ACLs, enabled Versioning, Static Website Hosting, and understood Storage Classes for cost optimization.