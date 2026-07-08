---
title: "Worklog Tuần 8"
date: 2026-06-08
weight: 8
chapter: false
pre: " <b> 1.8. </b> "
---

**Phát triển các API mở rộng & phân quyền cho hệ thống SaaS HR Multi-tenant**
**Name:** Lê Mạnh Cường
**ID:** 2280600340

### Week 8 Objectives:

* Kiến trúc Cloud-Native & Zero-Trust: Triển khai toàn bộ hạ tầng mạng, bảo mật và lưu trữ cho dự án SaaS HR hoàn toàn bằng mã nguồn Terraform thủ công, đảm bảo không có kết nối nào được chấp nhận nếu không được cấp phép rõ ràng.
* Tối ưu chi phí cực hạn (FinOps): Ép chi phí vận hành từ mức tiêu chuẩn xuống còn khoảng 70 - 95 USD/tháng, duy trì dưới trần ngân sách 120 - 150 USD/tháng.
* Quản trị định danh & Bảo mật: Quản lý truy cập nhóm thông qua IAM Identity Center (bắt buộc MFA) và quản lý người dùng ứng dụng qua AWS Cognito.

### Tasks to be carried out this week:

| Day | Task | Start Date | Completion Date | Reference Material |
| --- | --- | --- | --- | --- |
| 1 | - Khóa tài khoản root và cấu hình - IAM Identity Center với MFA bắt buộc. <br> - Khởi tạo AWS Budgets với ngưỡng cảnh báo 100 USD. <br> - Thiết lập CloudTrail và Terraform remote state trên S3. | 06/08/2026 | 06/08/2026 | |
| 2 | - Xây dựng một VPC duy nhất chứa Public và Private Subnets trải trên hai AZ (ap-southeast-1a và 1b). <br> - Thiết kế mô hình mạng loại bỏ hoàn toàn NAT Gateway nhằm tiết kiệm chi phí 32.85 USD/tháng. | 06/09/2026 | 06/09/2026 | |
| 3 | - Khởi chạy RDS MySQL 8.0 (db.t4g.micro) chạy 24/7 trong Private Subnet. <br> - Lưu trữ các thông tin nhạy cảm dưới dạng SecureString tĩnh trong SSM Parameter Store hoàn toàn miễn phí. <br> - Gộp ba database (auth, tenant, hr) vào chung một instance để tối ưu tài nguyên. | 06/10/2026 | 06/10/2026 | |
| 4 | - Đẩy ba thư mục mã nguồn microservices lên Amazon ECR. <br> - Khởi chạy bốn task (bao gồm Redis) trên ECS Fargate Spot giúp giảm 70% chi phí máy chủ. <br> - Cấu hình Application Load Balancer (ALB) định tuyến đường dẫn tới các API. | 06/11/2026 | 06/11/2026 | |
| 5 | - Cấu hình WAF v2 Web ACL tại vùng us-east-1 để gắn vào CloudFront. <br> - Áp dụng các bộ quy tắc bảo vệ lõi, chống SQLi và giới hạn request. | 06/12/2026 | 06/12/2026 | |
| 6 | - Di chuyển luồng xác thực (Authentication) sang Cognito User Pools. <br> - Giữ lại database nội bộ cho mục đích phân quyền (Authorization) và quản lý tenant. | 06/13/2026 | 06/13/2026 | |
| 7 | - Khởi tạo S3 Bucket chặn truy cập công cộng, chỉ cho phép Origin Access Control (OAC) từ CloudFront. <br> - Đăng ký tên miền qua Route 53 và trỏ ALIAS về CloudFront. | 06/14/2026 | 06/14/2026 | |

### Bảng Tổng Hợp Thành Phần Kiến Trúc

![SaaS HR Multi-Tenant AWS Architecture](images/architecture.png)

| Tầng / Vùng | Dịch Vụ AWS | Vai Trò | Vị Trí Mạng |
| --- | --- | --- | --- |
| DNS (Global Edge) | Amazon Route 53 | Phân giải tên miền → CloudFront | Global (Edge) |
| CDN & Bảo mật (Edge) | Amazon CloudFront + AWS WAF | Cache tại biên, chống DDoS, lọc Web ACL (WAF quản lý tại us-east-1) | Global (Edge) |
| Hosting tĩnh (Region) | Amazon S3 | Phục vụ bản build React frontend (Truy cập riêng tư qua Origin Access Control - OAC) | Regional (ap-southeast-1) |
| Xác thực (Region) | AWS Cognito (User Pools) | Quản lý xác thực người dùng, phát hành JWT token (custom attribute: custom:tenant_id) | Regional (ap-southeast-1) |
| Quản lý khóa (Region) | AWS SSM Parameter Store | Lưu trữ cấu hình bí mật mã hóa dưới dạng SecureString (Tĩnh & Miễn phí) | Regional (ap-southeast-1) |
| Cân bằng tải (VPC) | Application Load Balancer (ALB) | Điều hướng theo đường dẫn `/api/v1/*` đến các target groups của ECS | Public Subnet (ap-southeast-1a / 1b) |
| Tính toán (VPC) | Amazon ECS Fargate Spot (4 Tasks) | Auth, Tenant, HR microservices + Redis (Pub/Sub broker) kết nối qua AWS Cloud Map | Public Subnet (ap-southeast-1a / 1b) |
| Giám sát SIEM/SOC (VPC) | EC2 t3.small Spot (Wazuh Manager) | Trung tâm giám sát an ninh & phân tích log tập trung (Cùng VPC, subnet riêng) | Public Subnet SOC (ap-southeast-1a, 10.0.3.0/24) |
| Cơ sở dữ liệu (VPC) | Amazon RDS MySQL (db.t4g.micro) | 1 instance chứa 3 database: auth_db, tenant_db, hr_db | Private Subnet (ap-southeast-1a / 1b) |
| Quản trị (Account) | AWS IAM Identity Center + CloudTrail + AWS Budgets | Quản lý SSO, kiểm toán hoạt động hệ thống và cảnh báo ngân sách ($100 alert) | Cấp độ Tài khoản |

### Bảng Chi Tiết FinOps & Tối Ưu Chi Phí

| Dịch Vụ AWS | Cấu Hình Chi Tiết | Chi Phí Tiêu Chuẩn (24/7) | Chi Phí Tối Ưu | Chiến Lược Tối Ưu |
| --- | --- | --- | --- | --- |
| AWS WAF | 1 Web ACL, 3 Managed Rules (Core, SQLi, IP Rep) | $8.60 | $8.60 | Gắn vào CloudFront để bảo vệ biên và ALB. |
| CloudFront & S3 | 100 GB Data Transfer Out, S3 Storage (React App) | $9.50 | $0.50 | S3 Static Hosting, CloudFront Free Tier (1TB miễn phí/tháng). |
| AWS ALB | 1 Load Balancer, 1 LCU | $22.27 | $22.27 | Thiết yếu cho điều hướng path-based target groups. |
| ECS Fargate | 4 Tasks (0.25 vCPU, 0.5 GB RAM mỗi task) | $32.40 | $9.72 | Fargate Spot (tiết kiệm 70% so với On-Demand). |
| RDS MySQL | 1 Instance db.t4g.micro (2 vCPU, 1GB RAM) + 20GB gp3 | $13.98 | $5.70 | Lập lịch tự động tắt (chạy 10h/ngày, Thứ 2 - Thứ 6). |
| EC2 (Wazuh) | 1 Instance t3.small (2 vCPU, 2GB RAM) + 30GB gp3 | $17.58 | $6.20 | EC2 Spot Instance + Tự động tắt ngoài giờ test. |
| AWS Cognito & SSM | Cognito User Pools + SSM Parameter Store | $0.00 | $0.00 | Free Tier hỗ trợ đến 50.000 MAU và lưu trữ tham số miễn phí. |
| NAT Gateway | 1 NAT Gateway (Yêu cầu VPC tiêu chuẩn) | $32.85 | $0.00 | Thiết kế VPC không cần NAT (ECS chạy trong public subnets). |
| Data Transfer/CloudWatch | Logs, băng thông liên AZ | $10.00 | $3.00 | Luân chuyển log & giữ lại tối đa 7 ngày. |
| **Tổng / Tháng** | | **$147.18** | **$56.99** | **Tổng tiết kiệm: ~61% ($90.19 tiết kiệm/tháng)** |

### Week 8 Achievements:

* Đã thiết lập nền tảng bảo mật vững chắc với IAM Identity Center, CloudTrail và AWS Budgets (cảnh báo 100 USD).
* Xây dựng thành công VPC loại bỏ NAT Gateway, cấu hình mạng Public/Private Subnets tối ưu chi phí.
* Vận hành RDS MySQL tối ưu tài nguyên (gộp 3 database) và bảo mật tham số với SSM Parameter Store.
* Triển khai thành công ECS Fargate Spot và ALB, giúp tiết kiệm đáng kể chi phí máy chủ.
* Áp dụng bảo mật biên xuất sắc thông qua AWS WAF, CloudFront và tích hợp AWS Cognito cho luồng xác thực.
* Hoàn thiện chiến lược FinOps với tổng tiết kiệm ước tính 61% (giảm từ 147.18 USD xuống còn 56.99 USD/tháng).
