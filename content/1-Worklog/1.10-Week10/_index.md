---
title: "Week 10 Worklog"
date: 2026-06-22
weight: 10
chapter: false
pre: " <b> 1.10. </b> "
---

**Deploying Static Frontend & Configuring Application Load Balancer (ALB)**
**Name:** Lê Mạnh Cường
**ID:** 2280600340

### Week 10 Objectives:

* **Static Frontend Deployment:** Manually compile the React source code and configure static hosting on Amazon S3 with a Zero-Trust security policy (Block Public Access).
* **Backend Traffic Management:** Set up an Application Load Balancer (ALB) from scratch, allocate Target Groups, and write custom path-based routing rules for each microservice.
* **Manual Operation:** Ensure all network and storage infrastructure configurations are performed through direct actions on the AWS Console and AWS CLI, maintaining full control over the system architecture.

### Tasks to be carried out this week:

| Day | Task | Start Date | Completion Date | Reference Material |
| --- | --- | --- | --- | --- |
| 1 | - Initialize Load Balancer: Access EC2 Load Balancers, create an Application Load Balancer named `saashr-alb`. <br> - Configure Internet-facing routing and network association into VPC `saashr-vpc` at two public subnets `public-1a` and `public-1b`. <br> - Attach Security Group `sg-alb` (allow Ingress ports 80 and 443 from 0.0.0.0/0). | 06/22/2026 | 06/22/2026 | |
| 2 | - Set up Target Groups: Create 3 Target Groups (`tg-auth`, `tg-tenants`, `tg-hr`) with Target Type set to IP for containers on ECS Fargate. <br> - Manually configure health checks for each destination: `/api/v1/auth/health`, `/api/v1/tenants/health`, `/api/v1/hr/health`. | 06/23/2026 | 06/23/2026 | |
| 3 | - Write routing rules (Rules): Create a Listener on port 80 (HTTP) for the ALB. <br> - Set up Path-based routing rules: <br>&emsp; 1. Path `/api/v1/auth/*` forwards to `tg-auth`. <br>&emsp; 2. Path `/api/v1/tenants/*` forwards to `tg-tenants`. <br>&emsp; 3. Path `/api/v1/hr/*` forwards to `tg-hr`. | 06/24/2026 | 06/24/2026 | |
| 4 | - Compile Frontend: Check the React Frontend source code on the local machine. <br> - Manually run the build process (`npm run build`) to generate the `dist/` directory containing `index.html` and the `assets/` folder. Ensure the code runs stably before uploading to the Cloud. | 06/25/2026 | 06/25/2026 | |
| 5 | - Initialize S3 Bucket: Access AWS Console, create a new bucket named `saashr-frontend` (using ap-southeast-1 region). <br> - Security: Enable Block all public access to completely block direct access from the Internet, preparing for future CloudFront (OAC) integration. | 06/26/2026 | 06/26/2026 | |
| 6 | - Sync source code to S3: Open PowerShell/Terminal, use AWS CLI to execute the sync command: `aws s3 sync d:\SaaS-HR-Multi-tenant\frontend\dist\ s3://saashr-frontend-<account-id> --delete`. <br> - Verify on the S3 console (Objects tab) to ensure that the file structure (`index.html` and `assets/` folder) has been uploaded correctly. | 06/27/2026 | 06/27/2026 | |
| 7 | - Test overall system: Verify the Healthy/Unhealthy status of the Target Groups on the Console. <br> - Send simulated requests via the Load Balancer URL to verify ALB's ability to accurately route traffic into the internal microservices. | 06/28/2026 | 06/28/2026 | |

### Week 10 Achievements:

* **Load Balancers:** Created an Application Load Balancer named `saashr-alb` and successfully configured routing.
  ![Load Balancer](/images/week10_image1.png)
* **Target Groups for Microservices:** Created Target Groups (`tg-auth`, `tg-tenants`, `tg-hr`) with custom health check paths:
  * **tg-auth:**
    ![tg-auth](/images/week10_image2.png)
  * **tg-tenants:**
    ![tg-tenants](/images/week10_image3.png)
  * **tg-hr:**
    ![tg-hr](/images/week10_image4.png)
* **Listener Rules:** Set up ALB routing rules for each service endpoint path:
  ![Listener rules](/images/week10_image5.png)
* **S3 Buckets:** Created the secure frontend S3 bucket with all public access blocked:
  ![S3 Bucket Setup](/images/week10_image6.png)
* **Static Frontend:** Compiled and synchronized the frontend assets to the S3 bucket:
  ![Sync Frontend](/images/week10_image7.png)
  ![S3 Bucket Files](/images/week10_image8.png)
