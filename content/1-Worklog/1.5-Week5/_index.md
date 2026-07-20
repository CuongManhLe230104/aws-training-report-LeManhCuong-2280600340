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
| 1 | - AWS CLI: Install and configure `aws configure` (Access Key, Region, Output format JSON/Table) to interact with AWS via Terminal. <br> - Amazon Lightsail: Rapidly deploy open-source applications (WordPress, PrestaShop, Akaunting) and configure basic Networking. | 05/18/2026 | 05/18/2026 | <https://000011.awsstudygroup.com/> <br> <https://000045.awsstudygroup.com/> |
| 2 | - Amazon S3 & CloudFront: Configure Static Website Hosting for frontend source code. Integrate CloudFront as a CDN and set up Origin Access Control (OAC) to block direct access to S3. Enable Bucket Versioning to manage code file versions. | 05/19/2026 | 05/19/2026 | <https://000057.awsstudygroup.com/> |
| 3 | - IAM Role for EC2: Practice eliminating hard-coded static Access Keys in source code, replacing them by attaching IAM Roles directly to EC2 for secure automated authentication. <br> - Docker with AWS: Build Docker Images for local applications, write `docker-compose.yml` files to manage environment variables, deploy to EC2, and push images to Amazon ECR / Docker Hub. | 05/20/2026 | 05/20/2026 | <https://000015.awsstudygroup.com/> <br> <https://000048.awsstudygroup.com/> |
| 4 | - VM Import/Export: Practice packaging a virtual machine from a local virtualization environment (VMware Workstation), upload the disk image file (.ova/.vmdk) to S3, use AWS CLI to convert it into an Amazon Machine Image (AMI), and launch it as a fully functional EC2 instance. | 05/21/2026 | 05/21/2026 | <https://000014.awsstudygroup.com/> |
| 5 | - AWS Backup: Initialize a centralized Backup Plan to manage the backup lifecycle (Retention Period). Set up an automated resource backup schedule and configure Amazon SNS to push status notifications via email. Practice restoring data from backups. | 05/22/2026 | 05/22/2026 | <https://000013.awsstudygroup.com/> |
| 6 | - CloudWatch: Collect performance Metrics, configure CloudWatch Logs Insights to write application log query commands, and set up automated warning Alarms. <br> - AWS Budget: Create Cost Budgets and Usage Budgets, set warning thresholds (80% and 100%) via email when the system consumes costs or service running hours exceed the limit. | 05/23/2026 | 05/23/2026 | <https://000008.awsstudygroup.com/> <br> <https://000007.awsstudygroup.com/> |
| 7 | - Comprehensive Check & Resource Cleanup: <br> - System Review: Check the entire operational flow from the static Frontend (S3/CloudFront) connecting to container services running on the infrastructure. <br> - Cleanup: Execute the process of deleting created services (Delete S3 Buckets, ECR Images, Backup Vaults, remove CloudFront Distributions and Budget Alarms) to protect the account from unexpected costs. | 05/24/2026 | 05/24/2026 | Clean Up |

### Week 5 Achievements:

* **Module 11 (AWS CLI) & Module 45 (Lightsail):** Installed/configured AWS CLI for terminal management; used Amazon Lightsail for the rapid deployment of open-source applications.
* **Module 57 (S3 & CloudFront):** Configured Static Website Hosting, integrated CloudFront as a CDN, and set up Origin Access Control (OAC) to block direct access.
* **Module 48 (IAM Role) & Module 15 (Docker):** Attached IAM Roles to EC2 for secure authentication; built Docker Images, managed them via docker-compose.yml, and pushed to Amazon ECR.
* **Module 14 (VM Import/Export):** Packaged a local virtual machine, uploaded it to S3, and converted it to an Amazon Machine Image (AMI) to run on EC2.
* **Module 13 (AWS Backup):** Initialized a Backup Plan, set up automated schedules, configured SNS alerts, and successfully restored data.
* **Module 7 & 8 (CloudWatch & AWS Budget):** Configured log/metrics collection with CloudWatch; created Cost/Usage Budgets and set up automated budget alerts.