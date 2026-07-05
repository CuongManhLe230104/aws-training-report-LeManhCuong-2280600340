# BÁO CÁO TIẾN ĐỘ THỰC TẬP & QUÁ TRÌNH XÂY DỰNG WORKLOG

* **Họ và tên:** Lê Mạnh Cường
* **Mã số sinh viên:** 2280600340
* **Vị trí thực tập:** Workforce Bootcamp - First Cloud AI Journey 2026
* **Thời gian báo cáo:** Từ Tuần 1 đến Tuần 10

---

## I. TỔNG QUAN HỆ THỐNG WORKLOG WEBSITE

Hệ thống Worklog (Nhật ký thực tập) được xây dựng dựa trên nền tảng **Hugo (phiên bản v0.163.3 extended)** và giao diện mẫu chuyên nghiệp **hugo-theme-learn**. Đây là một nền tảng tạo trang web tĩnh (Static Site Generator) tối ưu, cho phép viết nội dung báo cáo bằng Markdown và tự động biên dịch thành các trang web HTML tĩnh.

Các công nghệ cốt lõi được áp dụng trong quá trình xây dựng và vận hành trang web Worklog bao gồm:
* **Hugo Framework:** Trình biên dịch trang web tĩnh tốc độ cao.
* **Đa ngôn ngữ (Multilingual):** Hỗ trợ song song hai phiên bản tiếng Anh (mặc định) và tiếng Việt (định tuyến qua `/vi/`).
* **Markdown Render Hooks:** Tự động hóa việc xử lý hình ảnh cục bộ. Bằng việc tùy biến tệp `render-image.html`, các đường dẫn ảnh tương đối sẽ tự động nhận diện `baseURL` để tránh lỗi hiển thị khi triển khai lên GitHub Pages.

---

## II. TÓM TẮT TIẾN ĐỘ VÀ KẾT QUẢ ĐẠT ĐƯỢC THEO TUẦN

### Tuần 1: Khởi đầu và Làm quen với Hạ tầng AWS
* **Mục tiêu:** Làm quen quy định thực tập, thiết lập tài khoản Free Tier và thử nghiệm các dịch vụ cơ bản (EC2, Lambda, RDS, Budgets).
* **Kết quả đạt được:**
  * Thiết lập thành công tài khoản AWS Free Tier và thiết lập cảnh báo ngân sách tránh phát sinh chi phí ngoài mong muốn.
  * Khởi chạy thành công máy chủ ảo EC2 chạy hệ điều hành Linux và thực hành truy cập từ xa qua SSH và CLI.
  * Tạo và chạy thành công hàm Serverless AWS Lambda kết nối với cơ sở dữ liệu quan hệ Amazon RDS.

### Tuần 2: Quản trị Định danh & Thiết lập Hạ tầng Mạng Cơ bản
* **Mục tiêu:** Nắm vững AWS IAM và cấu hình hạ tầng VPC cơ bản.
* **Kết quả đạt được:**
  * **Module 2 (AWS IAM):** Thực hành phân quyền chặt chẽ thông qua User, Group, Policy và Role. Cấu hình tính năng Switch Role cho OperatorUser nhằm tuân thủ nguyên tắc đặc quyền tối thiểu (Least Privilege).
  * **Module 3 (VPC & Networking):** Khởi tạo mạng riêng ảo VPC, phân chia subnet Public/Private, cấu hình Route Table, Internet Gateway (IGW) và NAT Gateway. Thiết lập Security Groups và Network ACLs bảo mật 2 lớp; sử dụng Reachability Analyzer để kiểm tra thông tuyến.

### Tuần 3: Dịch vụ Định danh Doanh nghiệp & Liên thông Mạng VPC
* **Mục tiêu:** Triển khai Microsoft Active Directory (AD) và cấu hình VPC Peering.
* **Kết quả đạt được:**
  * **Module 10 (Microsoft AD & RDGW):** Triển khai hệ thống Microsoft Active Directory trên AWS; cấu hình Remote Desktop Gateway (RDGW) để truy cập an toàn vào hệ thống nội bộ và thiết lập DNS phân giải tên miền.
  * **Module 19 (VPC Peering):** Thiết lập liên thông mạng VPC Peering giữa các vùng mạng khác nhau. Cấu hình bảng định tuyến và Cross-Peer DNS để đảm bảo các máy chủ giữa hai mạng phân giải được tên miền của nhau.

### Tuần 4: Phát triển Ứng dụng Web & Quản trị Lưu trữ
* **Mục tiêu:** Triển khai ứng dụng LAMP và cấu hình dịch vụ cơ sở dữ liệu RDS, lưu trữ S3.
* **Kết quả đạt được:**
  * **Module 4 (Network, Compute & LAMP):** Hoàn thiện liên thông mạng, áp dụng IAM Policy giới hạn quyền hạn truy cập theo vùng địa lý và triển khai ứng dụng Node.js CRUD trên mô hình máy chủ LAMP.
  * **Module 5 (Amazon RDS):** Khởi tạo RDS instance (MySQL/MariaDB), cấu hình backup tự động qua Snapshot, tìm hiểu cơ chế dự phòng Multi-AZ và mở rộng đọc (Read Replicas).
  * **Module 6 (Amazon S3):** Khởi tạo S3 Bucket, thiết lập chính sách bảo mật Bucket Policy/ACL, cấu hình Versioning bảo vệ dữ liệu và triển khai Static Website Hosting.

### Tuần 5: Công cụ Dòng lệnh CLI, Container hóa & Giám sát Hệ thống
* **Mục tiêu:** Tự động hóa qua AWS CLI, Docker, và thiết lập Backup, CloudWatch Logs, AWS Budget.
* **Kết quả đạt được:**
  * **Module 11 & 45:** Cài đặt và cấu hình AWS CLI; sử dụng dịch vụ Lightsail để triển khai nhanh các ứng dụng mẫu.
  * **Module 57:** Triển khai CloudFront CDN kết hợp với S3 Static Website, áp dụng Origin Access Control (OAC) để bảo mật tài nguyên lưu trữ tĩnh.
  * **Module 48 & 15:** Gắn IAM Role trực tiếp lên EC2 để ứng dụng truy cập tài nguyên không cần Access Key tĩnh; đóng gói ứng dụng bằng Docker và tải lên kho chứa Amazon ECR.
  * **Module 14 & 13:** Thực hành import máy ảo VM từ VMware lên EC2 dưới dạng AMI; thiết lập AWS Backup tự động hóa sao lưu và gửi cảnh báo qua SNS.
  * **Module 7 & 8:** Cấu hình giám sát hiệu năng qua CloudWatch Logs; thiết lập cảnh báo ngân sách chi tiết với AWS Budget.

### Tuần 6: Thiết kế và Xây dựng API Hệ thống SaaS HR
* **Mục tiêu:** Xây dựng và triển khai các API Microservices.
* **Kết quả đạt được:**
  * Thiết kế thành công hệ thống API quản trị thành viên và phân quyền vai trò (Owner, Admin, Member) cho dịch vụ Xác thực (auth-service).
  * Hoàn thiện các API quản lý hồ sơ nhân viên trong dịch vụ Nhân sự (hr-service), trích xuất thông tin doanh nghiệp (`tenant_id`) trực tiếp từ JWT Token để bảo đảm an toàn cô lập dữ liệu.
  * Xây dựng dịch vụ doanh nghiệp (tenant-service) và tích hợp toàn bộ hệ thống API thông qua Nginx API Gateway để bảo đảm cô lập Multi-tenancy.

### Tuần 7: Hiện đại hóa Ứng dụng & Kiến trúc Serverless
* **Mục tiêu:** Chuyển đổi sang kiến trúc Microservices Serverless, CI/CD và bảo mật Cognito.
* **Kết quả đạt được:**
  * **Module 50 & 51 (Migrate & CI/CD):** Phân rã Monolith và xây dựng đường ống CI/CD tự động phát hành ứng dụng (Auto-release).
  * **Module 52 & 53 (Microservices & Data):** Thiết kế các microservices độc lập và tái cấu trúc luồng dữ liệu phân tán.
  * **Module 54 & 55 (Messaging & SPA):** Cấu hình hệ thống nhắn tin bất đồng bộ, định tuyến sự kiện và xây dựng ứng dụng Frontend Single Page Application (SPA).
  * **Module 47 & 56:** Cấu hình AWS Step Functions để điều phối quy trình công việc phức tạp và tích hợp các dịch vụ trí tuệ nhân tạo (AI Services).
  * **Module 78 & 79:** Viết các hàm AWS Lambda kết nối với DynamoDB và S3; cấu hình API Gateway để tiếp nhận request từ Frontend.
  * **Module 80 & 81:** Đóng gói ứng dụng Serverless bằng AWS SAM; thiết lập xác thực người dùng tập trung bằng Amazon Cognito.

### Tuần 8: Triển khai Hạ tầng Khai báo (IaC) & Bảo mật Zero-Trust nâng cao
* **Mục tiêu:** Tự động hóa toàn bộ hạ tầng bằng Terraform và tối ưu hóa chi phí FinOps.
* **Kết quả đạt được:**
  * Viết toàn bộ mã nguồn Terraform để khởi tạo VPC, ECS Fargate, ALB, RDS, WAF, CloudFront, Route 53 từ con số 0.
  * **Tối ưu chi phí FinOps:** Thiết kế mạng loại bỏ NAT Gateway (chạy ECS trong Public Subnets), áp dụng ECS Fargate Spot (tiết kiệm 70%) và lập lịch tự động tắt RDS ngoài giờ làm việc. Giảm tổng chi phí vận hành từ 147.18 USD xuống còn 56.99 USD/tháng (tiết kiệm 61%).
  * Tích hợp AWS WAF v2 chống tấn công SQLi, bảo vệ biên thông qua Amazon CloudFront CDN và định tuyến Route 53.

### Tuần 9: Bảo mật Credentials Chặng cuối & So sánh VPC Link
* **Mục tiêu:** Bảo vệ thông tin nhạy cảm và nghiên cứu kết nối mạng API Gateway.
* **Kết quả đạt được:**
  * Ứng dụng AWS Secrets Manager để lưu trữ thông tin đăng nhập RDS, viết hàm Lambda tự động xoay vòng mật khẩu (Rotation) sau mỗi 30 ngày để đảm bảo an toàn tuyệt đối chặng cuối (last-mile credentials).
  * Đánh giá chi tiết cơ chế hoạt động của VPC Link: Đối chiếu Private Integration của REST API (dựa trên AWS PrivateLink kết hợp NLB) và HTTP API (dựa trên AWS Hyperplane hỗ trợ ALB/Cloud Map).

### Tuần 10: Vận hành Thực tế và Triển khai Frontend lên S3
* **Mục tiêu:** Đưa Frontend tĩnh lên Cloud và cấu hình ALB điều phối lưu lượng.
* **Kết quả đạt được:**
  * Biên dịch mã nguồn React Frontend thành sản phẩm tĩnh, khởi tạo S3 Bucket chặn hoàn toàn truy cập trực tiếp từ Internet, đồng bộ hóa mã nguồn tĩnh bằng lệnh `aws s3 sync`.
  * Khởi tạo bộ cân bằng tải Application Load Balancer (saashr-alb) và cấu hình các quy tắc định tuyến thông minh dựa trên đường dẫn (Path-based Routing): `/api/v1/auth/*` chuyển tới tg-auth, `/api/v1/tenants/*` chuyển tới tg-tenants, và `/api/v1/hr/*` chuyển tới tg-hr.

---

## III. KẾT LUẬN & ĐÁNH GIÁ CHUNG

Qua 10 tuần học tập và triển khai thực tế trên hạ tầng đám mây AWS, hệ thống báo cáo thực tập (Worklog) và dự án SaaS HR Multi-tenant đã được hoàn thiện với đầy đủ các tiêu chuẩn kỹ thuật cao:
1. **Về mặt hạ tầng mạng & bảo mật:** Áp dụng triệt để nguyên lý đặc quyền tối thiểu (Least Privilege) của IAM, thiết kế mạng riêng biệt (VPC, Subnets, Security Groups), bảo vệ dữ liệu với Secrets Manager và tích hợp WAF/CloudFront ở biên để phòng chống tấn công.
2. **Về mặt tối ưu chi phí (FinOps):** Triển khai thành công các giải pháp tiết kiệm tối đa như ECS Fargate Spot, RDS scheduling và VPC không NAT, giúp hệ thống vận hành ổn định với chi phí thấp nhất.
3. **Về mặt công nghệ Worklog:** Website báo cáo hoạt động nhanh, mượt mà nhờ Hugo. Giải quyết triệt để vấn đề vỡ giao diện và lỗi đường dẫn ảnh thông qua cơ chế Render Hooks tự động tiền tố đường dẫn ảnh phù hợp với GitHub Pages.

---

## IV. BẢNG KÝ DUYỆT BÁO CÁO

| Người duyệt báo cáo | Người làm báo cáo |
| :---: | :---: |
| *(Ký và ghi rõ họ tên)* | **Lê Mạnh Cường** |
