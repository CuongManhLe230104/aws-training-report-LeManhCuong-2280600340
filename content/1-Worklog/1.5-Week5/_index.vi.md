---
title: "Worklog Tuần 5"
date: 2026-05-18
weight: 5
chapter: false
pre: " <b> 1.5. </b> "
---

**Explore AWS Services**
**Name:** Lê Mạnh Cường
**ID:** 2280600340

### Week 5 Objectives:

* Giao diện & Triển khai nhanh: Thành thạo AWS CLI để quản trị bằng dòng lệnh và sử dụng Amazon Lightsail để vận hành nhanh các ứng dụng mẫu.
* Lưu trữ & Bảo mật: Cấu hình hệ thống lưu trữ phân phối bảo mật với S3 và CloudFront; áp dụng IAM Role để phân quyền ứng dụng an toàn.
* Vận hành & Giám sát: Đóng gói ứng dụng với Docker, xử lý di chuyển máy ảo (VM Import/Export), tự động hóa sao lưu (AWS Backup), thiết lập giám sát (CloudWatch) và kiểm soát ngân sách (AWS Budget).

### Tasks to be carried out this week:

| Day | Task | Start Date | Completion Date | Reference Material |
| --- | --- | --- | --- | --- |
| 1 | - Module 11 (AWS CLI): Cài đặt và cấu hình aws configure (Access Key, Region, Output format JSON/Table) để tương tác với AWS qua Terminal. <br> - Module 45 (Amazon Lightsail): Triển khai nhanh các ứng dụng mã nguồn mở (WordPress, PrestaShop, Akaunting) và cấu hình Networking cơ bản. | 05/18/2026 | 05/18/2026 | <https://000011.awsstudygroup.com/> <br> <https://000045.awsstudygroup.com/> |
| 2 | - Module 57 (Amazon S3 & CloudFront): Cấu hình Static Website Hosting cho mã nguồn frontend. Tích hợp CloudFront làm CDN và thiết lập Origin Access Control (OAC) để chặn truy cập trực tiếp vào S3. Kích hoạt Bucket Versioning để quản lý các phiên bản file code. | 05/19/2026 | 05/19/2026 | <https://000057.awsstudygroup.com/> |
| 3 | - Module 48 (IAM Role cho EC2): Thực hành loại bỏ việc gán cứng Access Key tĩnh trong mã nguồn, thay thế bằng cách gắn IAM Role trực tiếp lên EC2 để ứng dụng tự động xác thực an toàn. <br> - Module 15 (Docker với AWS): Build Docker Image cho ứng dụng ở local, viết file docker-compose.yml để quản trị biến môi trường, triển khai lên EC2 và push image lên Amazon ECR / Docker Hub. | 05/20/2026 | 05/20/2026 | <https://000015.awsstudygroup.com/> <br> <https://000048.awsstudygroup.com/> |
| 4 | - Module 14 (VM Import/Export): Thực hành đóng gói một máy ảo từ môi trường ảo hóa cục bộ (VMware Workstation), upload file ảnh đĩa (.ova/.vmdk) lên S3, dùng AWS CLI để convert thành Amazon Machine Image (AMI) và launch thành máy chủ EC2 hoàn chỉnh. | 05/21/2026 | 05/21/2026 | <https://000014.awsstudygroup.com/> |
| 5 | - Module 13 (AWS Backup): Khởi tạo một Backup Plan tập trung để quản lý vòng đời sao lưu (Retention Period). Thiết lập lịch trình tự động sao lưu tài nguyên và cấu hình Amazon SNS để đẩy thông báo trạng thái qua email. Thực hành khôi phục (Restore) dữ liệu từ bản backup. | 05/22/2026 | 05/22/2026 | <https://000013.awsstudygroup.com/> |
| 6 | - Module 8 (CloudWatch): Thu thập Metrics hiệu năng, cấu hình CloudWatch Logs Insights để viết câu lệnh truy vấn log ứng dụng, thiết lập Alarms cảnh báo tự động. <br> - Module 7 (AWS Budget): Tạo Cost Budget và Usage Budget, thiết lập ngưỡng cảnh báo (80% và 100%) qua email khi hệ thống tiêu hao chi phí hoặc số giờ chạy dịch vụ vượt định mức. | 05/23/2026 | 05/23/2026 | <https://000008.awsstudygroup.com/> <br> <https://000007.awsstudygroup.com/> |
| 7 | - Kiểm tra tổng thể & Giải phóng tài nguyên: <br> - Review hệ thống: Kiểm tra toàn bộ luồng vận hành từ Frontend tĩnh (S3/CloudFront) kết nối tới các dịch vụ container chạy trên hạ tầng. <br> - Cleanup: Thực hiện quy trình xóa bỏ các dịch vụ đã tạo (Xóa S3 Buckets, ECR Images, Backup Vaults, gỡ bỏ CloudFront Distributions và Budget Alarms) để bảo vệ tài khoản khỏi phát sinh chi phí ngoài ý muốn. | 05/24/2026 | 05/24/2026 | Clean Up |

### Week 5 Achievements:

* **Module 11 (AWS CLI) & Module 45 (Lightsail):** Cài đặt/cấu hình AWS CLI để quản trị qua Terminal; sử dụng Amazon Lightsail triển khai nhanh các ứng dụng mã nguồn mở.
* **Module 57 (S3 & CloudFront):** Cấu hình Static Website Hosting, tích hợp CloudFront làm CDN và thiết lập Origin Access Control (OAC) chặn truy cập trực tiếp.
* **Module 48 (IAM Role) & Module 15 (Docker):** Gắn IAM Role trực tiếp lên EC2 để xác thực an toàn; build Docker Image, quản trị bằng docker-compose.yml và push lên Amazon ECR.
* **Module 14 (VM Import/Export):** Đóng gói máy ảo cục bộ, upload lên S3 và convert thành Amazon Machine Image (AMI) để chạy trên EC2.
* **Module 13 (AWS Backup):** Khởi tạo Backup Plan, thiết lập lịch trình tự động, cấu hình cảnh báo SNS và khôi phục dữ liệu thành công.
* **Module 7 & 8 (CloudWatch & AWS Budget):** Cấu hình thu thập log/metrics với CloudWatch; tạo Cost/Usage Budget và thiết lập cảnh báo ngân sách tự động.
