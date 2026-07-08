---
title: "Worklog Tuần 4"
date: 2026-05-11
weight: 4
chapter: false
pre: " <b> 1.4. </b> "
---

**Explore AWS Services**
**Name:** Lê Mạnh Cường
**ID:** 2280600340

### Week 4 Objectives:

* Hạ tầng: Khởi tạo và cấu hình môi trường mạng (VPC, Security Group) cho các loại hệ điều hành khác nhau.
* Quản trị: Thành thạo các thao tác vận hành máy chủ ảo (EC2) như thay đổi cấu hình, sao lưu (Snapshot) và đóng gói (AMI).
* Bảo mật & Phục hồi: Thực hành các phương thức truy cập thay thế khi mất thông tin xác thực (Key Pair).
* Triển khai: Cài đặt môi trường Web Server (LAMP/XAMPP) và triển khai ứng dụng Node.js thực tế.
* Quản trị Amazon RDS: Hiểu về dịch vụ cơ sở dữ liệu quan hệ (Relational Database), cách cấu hình bảo mật, sao lưu và tính sẵn sàng cao (Multi-AZ).
* Lưu trữ với Amazon S3 (Module 6): Hiểu về lưu trữ đối tượng (Object Storage), quản lý quyền truy cập và các tính năng nâng cao như Hosting Website tĩnh, Versioning.

### Tasks to be carried out this week:

| Day | Task | Start Date | Completion Date | Reference Material |
| --- | --- | --- | --- | --- |
| 1 | - Thực hiện các bước chuẩn bị (Preparation). <br> - Triển khai Microsoft AD Deployment trên AWS. <br> - Thiết lập kết nối bảo mật đến RDGW. <br> - Cấu hình hệ thống phân giải tên miền nội bộ (Setup DNS). | 05/11/2026 | 05/11/2026 | <https://000004.awsstudygroup.com/> |
| 2-3 | - Kiểm tra Prerequisites & Cấu hình Network ACL. <br> - Khởi tạo kết nối VPC Peering giữa các vùng mạng. <br> - Cập nhật Route Tables cho các Subnet. <br> - Thiết lập Cross-Peer DNS để gọi dịch vụ qua hostname. <br> - Áp dụng IAM Policy để giới hạn quyền hạn theo Region và Instance Type. <br> - Triển khai ứng dụng Node.js CRUD trên nền tảng LAMP/XAMPP. | 05/12/2026 | 05/13/2026 | <https://000004.awsstudygroup.com/> |
| 4-5 | - Chuẩn bị hạ tầng RDS: Tạo VPC, EC2 Security Group, RDS Security Group và DB Subnet Group. <br> - Khởi tạo RDS: Tạo instance cơ sở dữ liệu (MySQL/MariaDB/PostgreSQL). <br> - Triển khai ứng dụng kết nối tới RDS Database. <br> - Thực hành Backup & Restore: Tạo DB Snapshot và khôi phục dữ liệu. <br> - Tìm hiểu cơ chế Multi-AZ (High Availability) và Read Replicas (Scalability). | 05/14/2026 | 05/15/2026 | <https://000005.awsstudygroup.com/> |
| 6-7 | - Tạo S3 Bucket, thực hành Upload/Download đối tượng. <br> - Cấu hình Bucket Policy và ACL để quản lý quyền truy cập. <br> - Kích hoạt Versioning (Quản lý phiên bản) và Static Website Hosting. <br> - Tìm hiểu các loại lưu trữ (Storage Classes) để tối ưu chi phí. <br> - Kiểm tra luồng dữ liệu: App (EC2) -> DB (RDS) -> Media (S3). | 05/16/2026 | 05/17/2026 | <https://000006.awsstudygroup.com/> |

### Week 4 Achievements:

* **Module 4 (Network, Compute & LAMP):** Hoàn thiện môi trường VPC Peering, thiết lập Cross-Peer DNS, áp dụng IAM Policy giới hạn quyền hạn theo Region/Instance Type, và triển khai thành công ứng dụng Node.js CRUD trên nền tảng LAMP/XAMPP.
* **Module 5 (Amazon RDS):** Chuẩn bị hạ tầng và khởi tạo thành công RDS instance (MySQL/MariaDB/PostgreSQL); thực hành tính năng Backup & Restore (DB Snapshot) và nắm vững cơ chế Multi-AZ, Read Replicas.
* **Module 6 (Amazon S3):** Quản trị lưu trữ đối tượng với S3 Bucket, cấu hình Bucket Policy/ACL bảo mật, kích hoạt Versioning, Static Website Hosting và hiểu rõ các lớp lưu trữ (Storage Classes) để tối ưu chi phí.
