---
title: "Week 6 Worklog"
date: 2026-05-25
weight: 6
chapter: false
pre: " <b> 1.6. </b> "
---

**Developing Extended APIs & Authorization for SaaS HR Multi-tenant System**
**Name:** Lê Mạnh Cường
**ID:** 2280600340

### Week 6 Objectives:

* Authentication Service (auth-service): Design and build APIs for enterprise member management (Workspace Users), role authorization (Owner, Admin, Member), and access control.
* HR Service (hr-service): Develop APIs to update employee profiles/positions and remove employees from the tenant's system, ensuring data safety constraints.
* Tenant Service (tenant-service): Develop APIs to view enterprise information (for tenant employees) and update basic information (logo, enterprise name) for the Owner.

### Tasks to be carried out this week:

| Day | Task | Start Date | Completion Date | Reference Material |
| --- | --- | --- | --- | --- |
| 1 | Analyze & design database for Auth Service: <br> - Survey existing users and user_tenants tables. <br> - Design specifications for Workspace Users management APIs: List users in the current tenant, update roles, and evict members. | 05/25/2026 | 05/25/2026 | |
| 2 | Logic specification and implementation of Auth Service APIs: <br> - Build CRUD functions to query data from the user_tenants table. <br> - Build processing routers, integrate authorization middleware (only Owner or Admin can modify roles or evict users from the tenant). | 05/26/2026 | 05/26/2026 | |
| 3 | Analyze & design update/delete employee APIs for HR Service: <br> - Survey data fields needed to update employee profiles (EmployeeUpdate). <br> - Design update and delete endpoints. <br> - Design security constraints: Only allow accounts with 'admin' or 'owner' roles to modify or delete employee information. | 05/27/2026 | 05/27/2026 | |
| 4 | Logic specification and implementation of HR Service APIs: <br> - Write CRUD functions to update profiles (update_employee) and delete employees (delete_employee). <br> - Set up API endpoints in the hr.py router. <br> - Extract tenant_id from the JWT token to ensure HR information isolation between tenants. | 05/28/2026 | 05/28/2026 | |
| 5 | Analyze & design Tenant configuration management APIs: <br> - Design APIs to view enterprise configurations and update the enterprise logo/name. <br> - Determine the current Tenant DB structure and the data transmission flow between the Client and Tenant Service. | 05/29/2026 | 05/29/2026 | |
| 6 | Logic specification and implementation of Tenant Service APIs: <br> - Implement the tenants.py router to handle view and update configuration requests. <br> - Use the tenant_id extracted from the user's authentication token to accurately identify the queried enterprise, preventing data leaks or unauthorized cross-tenant updates. | 05/30/2026 | 05/30/2026 | |
| 7 | Comprehensive testing of newly developed APIs: <br> - Build test cases using Postman / cURL to simulate API call flows through the Nginx API Gateway. <br> - Test Role-based Access Control (RBAC) and data isolation (Multi-tenancy). <br> - Clean up test data and prepare the production environment. | 05/31/2026 | 05/31/2026 | |

### Week 6 Achievements:

* Successfully designed and built APIs for enterprise member management, role authorization (Owner, Admin, Member), and access control for the Authentication Service (auth-service).
  ![SaaS HR Auth Service API](images/auth_service_1.png)
* Completely developed APIs for updating profiles/positions and removing employees for the HR Service (hr-service), successfully integrating `tenant_id` extraction from JWT tokens to ensure data isolation.
  ![SaaS HR Core Service API](images/core_service.png)
* Completed the development of APIs for the Tenant Service (tenant-service) to securely view and update enterprise configurations.
  ![SaaS HR Tenant Service API](images/tenant_service.png)
* Successfully tested the entire API system via the Nginx API Gateway, verifying that Role-Based Access Control (RBAC) and Multi-tenancy data isolation function accurately.