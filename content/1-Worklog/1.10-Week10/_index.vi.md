---
title: "Worklog Tuần 10"
date: 2026-06-22
weight: 10
chapter: false
pre: " <b> 1.10. </b> "
---

**Triển khai Frontend tĩnh & Cấu hình Application Load Balancer (ALB)**
**Name:** Lê Mạnh Cường
**ID:** 2280600340

### Mục tiêu tuần 10:

* **Triển khai Frontend tĩnh:** Tự tay biên dịch mã nguồn React và cấu hình lưu trữ tĩnh trên Amazon S3 với chính sách bảo mật Zero-Trust (Block Public Access).
* **Quản lý lưu lượng Backend:** Thiết lập Application Load Balancer (ALB) từ con số không, phân bổ các Target Group và tự viết các quy tắc định tuyến (Path-based Routing) cho từng microservice.
* **Vận hành thủ công:** Đảm bảo mọi cấu hình hạ tầng mạng và lưu trữ đều được thực hiện thông qua thao tác trực tiếp trên AWS Console và giao diện dòng lệnh (AWS CLI), kiểm soát hoàn toàn kiến trúc hệ thống.

### Các công việc cần triển khai trong tuần này:

| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --- | --- | --- | --- |
| 2 | - Khởi tạo Load Balancer: Truy cập EC2 Load Balancers, tạo Application Load Balancer với tên `saashr-alb`. <br> - Cấu hình định tuyến Internet-facing và liên kết mạng vào VPC `saashr-vpc` tại 2 subnet public-1a và public-1b. <br> - Gắn Security Group `sg-alb` (mở Ingress cổng 80 và 443 từ 0.0.0.0/0). | 06/22/2026 | 06/22/2026 | |
| 3 | - Thiết lập Target Groups: Tạo 3 Target Group (`tg-auth`, `tg-tenants`, `tg-hr`) với loại Target là IP dành cho các container trên ECS Fargate. <br> - Cấu hình Health check thủ công cho từng đích đến: `/api/v1/auth/health`, `/api/v1/tenants/health`, `/api/v1/hr/health`. | 06/23/2026 | 06/23/2026 | |
| 4 | - Viết quy tắc định tuyến (Rules): Tạo Listener trên cổng 80 (HTTP) cho ALB. <br> - Thiết lập các quy tắc Path-based routing: <br>&emsp; 1. Path `/api/v1/auth/*` Chuyển tiếp tới `tg-auth`. <br>&emsp; 2. Path `/api/v1/tenants/*` Chuyển tiếp tới `tg-tenants`. <br>&emsp; 3. Path `/api/v1/hr/*` Chuyển tiếp tới `tg-hr`. | 06/24/2026 | 06/24/2026 | |
| 5 | - Biên dịch Frontend: Kiểm tra mã nguồn Frontend React trên máy cục bộ. <br> - Tự tay chạy tiến trình build (`npm run build`) để tạo ra thư mục `dist/` chứa file `index.html` và thư mục `assets/`. Đảm bảo code chạy ổn định trước khi đưa lên Cloud. | 06/25/2026 | 06/25/2026 | |
| 6 | - Khởi tạo S3 Bucket: Truy cập AWS Console, tạo bucket mới với tên định dạng: `saashr-frontend` tại Region ap-southeast-1. <br> - Bảo mật: Kích hoạt tính năng Block all public access để chặn hoàn toàn việc truy cập trực tiếp từ Internet, chuẩn bị cho việc tích hợp CloudFront (OAC) sau này. | 06/26/2026 | 06/26/2026 | |
| 7 | - Đồng bộ mã nguồn lên S3: Mở PowerShell/Terminal, sử dụng AWS CLI để thực thi lệnh đồng bộ dữ liệu: `aws s3 sync d:\SaaS-HR-Multi-tenant\frontend\dist\ s3://saashr-frontend-<account-id> --delete`. <br> - Kiểm tra lại trên giao diện S3 (tab Objects) để đảm bảo cấu trúc file (`index.html` và thư mục `assets/`) đã được upload chính xác. | 06/27/2026 | 06/27/2026 | |
| CN | - Kiểm thử hệ thống tổng thể: Kiểm tra trạng thái Healthy/Unhealthy của các Target Group trên Console. <br> - Gửi các request giả lập qua URL của Load Balancer để xác minh khả năng phân luồng dữ liệu chính xác của ALB vào các microservices nội bộ. | 06/28/2026 | 06/28/2026 | |

### Kết quả đạt được (Week 10 Achievements):

* **Load balancers (Cân bằng tải):** Khởi tạo bộ cân bằng tải ứng dụng `saashr-alb` định tuyến Internet-facing kết nối đồng thời với 2 AZ khác nhau và được bảo mật bởi `sg-alb`.
  ![Load Balancer](/images/week10_image1.png)
* **Target Group (Nhóm đích):** Thiết lập các nhóm đích tương ứng cho các dịch vụ Authentication, Tenants, và HR, đi kèm với cấu hình endpoints kiểm tra sức khỏe:
  * **tg-auth:**
    ![tg-auth](/images/week10_image2.png)
  * **tg-tenants:**
    ![tg-tenants](/images/week10_image3.png)
  * **tg-hr:**
    ![tg-hr](/images/week10_image4.png)
* **Listener rules (Quy tắc định tuyến):** Cài đặt Listener quy tắc cổng 80 cho ALB để thực hiện định tuyến dựa trên đường dẫn gọi API (Path-based Routing):
  ![Listener rules](/images/week10_image5.png)
* **S3 - Buckets:** Tạo thành công bucket `saashr-frontend` chạy tại Region ap-southeast-1, chặn hoàn toàn truy cập public từ môi trường ngoài để thực thi mô hình Zero-Trust.
  ![S3 Bucket Setup](/images/week10_image6.png)
* **Static frontend (Giao diện tĩnh):** Biên dịch thành công mã nguồn React và đồng bộ hóa trực tiếp lên S3 qua lệnh `aws s3 sync`:
  ![Sync Frontend](/images/week10_image7.png)
  ![S3 Objects Structure](/images/week10_image8.png)
