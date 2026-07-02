---
title: "Week 5 Worklog"
date: 2026-05-18
weight: 5
chapter: false
pre: " <b> 1.5. </b> "
---

**Explore AWS Services**
**Name:** Lê Mạnh Cường
**ID:** 2280600340

### Week 5 Objectives:

* Interface & Rapid Deployment: Master AWS CLI for command-line administration and use Amazon Lightsail to quickly deploy sample applications.
* Storage & Security: Configure a secure distributed storage system with S3 and CloudFront; apply IAM Roles for secure application authorization.
* Operations & Monitoring: Package applications with Docker, handle virtual machine migration (VM Import/Export), automate backups (AWS Backup), set up monitoring (CloudWatch), and control budgets (AWS Budget).

### Tasks to be carried out this week:

| Day | Task | Start Date | Completion Date | Reference Material |
| --- | --- | --- | --- | --- |
| 1 | - Module 11 (AWS CLI): Install and configure `aws configure` (Access Key, Region, Output format JSON/Table) to interact with AWS via Terminal. <br> - Module 45 (Amazon Lightsail): Rapidly deploy open-source applications (WordPress, PrestaShop, Akaunting) and configure basic Networking. | 05/18/2026 | 05/18/2026 | <https://000011.awsstudygroup.com/> <br> <https://000045.awsstudygroup.com/> |
| 2 | - Module 57 (Amazon S3 & CloudFront): Configure Static Website Hosting for frontend source code. Integrate CloudFront as a CDN and set up Origin Access Control (OAC) to block direct access to S3. Enable Bucket Versioning to manage code file versions. | 05/19/2026 | 05/19/2026 | <https://000057.awsstudygroup.com/> |
| 3 | - Module 48 (IAM Role for EC2): Practice eliminating hard-coded static Access Keys in source code, replacing them by attaching IAM Roles directly to EC2 for secure automated authentication. <br> - Module 15 (Docker with AWS): Build Docker Images for local applications, write `docker-compose.yml` files to manage environment variables, deploy to EC2, and push images to Amazon ECR / Docker Hub. | 05/20/2026 | 05/20/2026 | <https://000015.awsstudygroup.com/> <br> <https://000048.awsstudygroup.com/> |
| 4 | - Module 14 (VM Import/Export): Practice packaging a virtual machine from a local virtualization environment (VMware Workstation), upload the disk image file (.ova/.vmdk) to S3, use AWS CLI to convert it into an Amazon Machine Image (AMI), and launch it as a fully functional EC2 instance. | 05/21/2026 | 05/21/2026 | <https://000014.awsstudygroup.com/> |
| 5 | - Module 13 (AWS Backup): Initialize a centralized Backup Plan to manage the backup lifecycle (Retention Period). Set up an automated resource backup schedule and configure Amazon SNS to push status notifications via email. Practice restoring data from backups. | 05/22/2026 | 05/22/2026 | <https://000013.awsstudygroup.com/> |
| 6 | - Module 8 (CloudWatch): Collect performance Metrics, configure CloudWatch Logs Insights to write application log query commands, and set up automated warning Alarms. <br> - Module 7 (AWS Budget): Create Cost Budgets and Usage Budgets, set warning thresholds (80% and 100%) via email when the system consumes costs or service running hours exceed the limit. | 05/23/2026 | 05/23/2026 | <https://000008.awsstudygroup.com/> <br> <https://000007.awsstudygroup.com/> |
| 7 | - Comprehensive Check & Resource Cleanup: <br> - System Review: Check the entire operational flow from the static Frontend (S3/CloudFront) connecting to container services running on the infrastructure. <br> - Cleanup: Execute the process of deleting created services (Delete S3 Buckets, ECR Images, Backup Vaults, remove CloudFront Distributions and Budget Alarms) to protect the account from unexpected costs. | 05/24/2026 | 05/24/2026 | Clean Up |

### Week 5 Achievements:

* Mastered AWS CLI for command-line administration and used Amazon Lightsail to quickly deploy sample applications.
* Successfully configured a secure distributed storage system with S3 and CloudFront; applied IAM Roles for secure application authorization.
* Successfully packaged applications with Docker, handled virtual machine migration (VM Import/Export), automated backups (AWS Backup), set up monitoring (CloudWatch), and controlled budgets (AWS Budget).