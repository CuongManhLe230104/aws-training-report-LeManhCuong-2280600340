---
title: "Bản đề xuất"
date: 2026-06-27
weight: 2
chapter: false
pre: " <b> 2. </b> "
---

# Nền tảng SaaS HR Đa Tổ Chức (Multi-Tenant) trên AWS
## Giải pháp Quản trị Nhân sự Điện toán Đám mây Bảo mật, Khả mở và Tối ưu Chi phí

### 1. Tóm tắt điều hành
Nền tảng SaaS HR Multi-Tenant là một giải pháp quản lý nhân sự đám mây hiện đại được thiết kế dành cho các doanh nghiệp vừa và nhỏ (SMEs). Nền tảng áp dụng cơ chế cô lập dữ liệu khách hàng (multi-tenant isolation) nghiêm ngặt, đảm bảo thông tin nhân viên, phòng ban và bảng lương của từng công ty được phân tách hoàn toàn dựa trên mô hình bảo mật Zero-Trust. Hệ thống sử dụng kiến trúc microservices viết bằng FastAPI kết hợp giao diện React, chạy trên các dịch vụ quản trị của AWS như ECS Fargate, ALB, RDS MySQL Multi-AZ, S3, CloudFront, Cognito, SQS, Secrets Manager và CloudWatch nhằm đạt hiệu năng cao, khả năng tự động mở rộng và hiệu quả chi phí vượt trội.

---

### 2. Tuyên bố vấn đề

#### Vấn đề hiện tại
Các doanh nghiệp vừa và nhỏ (SMEs) rất cần các hệ thống quản trị nhân sự ổn định nhưng gặp khó khăn lớn về chi phí đầu tư và năng lực kỹ thuật để tự triển khai, vận hành các máy chủ chuyên dụng. Các giải pháp đơn tổ chức (single-tenant) truyền thống thường tốn kém và khó mở rộng, trong khi các hệ thống đa tổ chức (multi-tenant) cơ bản lại dễ gặp rủi ro về rò rỉ dữ liệu chéo giữa các khách hàng và cấu hình bảo mật lỏng lẻo.

#### Giải pháp
Giải pháp được đề xuất là một nền tảng SaaS HR đa tổ chức (multi-tenant) được quản trị hoàn toàn trên hạ tầng đám mây AWS. Hệ thống thực hiện cô lập dữ liệu ở tầng ứng dụng bằng cách trích xuất trường thông tin `tenant_id` từ các chữ ký token RS256 JWT an toàn. Hạ tầng hệ thống chạy hoàn toàn ở dạng Serverless và có tính sẵn sàng cao, sử dụng ECS Fargate để tính toán và RDS MySQL Multi-AZ làm cơ sở dữ liệu quan hệ.

#### Lợi ích và hoàn vốn đầu tư (ROI)
- **Không tốn chi phí vận hành hạ tầng:** Sử dụng công nghệ container serverless (AWS Fargate) giúp loại bỏ việc vá lỗi hay quản trị máy chủ ảo thủ công.
- **Cô lập dữ liệu nghiêm ngặt:** Đảm bảo tính tuân thủ bảo mật thông qua việc cách ly dữ liệu ở cả tầng ứng dụng và mạng riêng ảo.
- **Tiết kiệm chi phí tối đa:** Áp dụng các chiến lược FinOps thông minh (loại bỏ NAT Gateway, lập lịch bật/tắt RDS ngoài giờ, chạy ECS Fargate Spot) giúp giảm 61% chi phí vận hành hàng tháng từ $132.80 USD xuống chỉ còn $51.70 USD.
- **Thời gian hoàn vốn nhanh:** Ước tính từ 3–6 tháng nhờ cắt giảm nhân lực vận hành hệ thống và tối ưu hóa tài nguyên đám mây.

---

### 3. Kiến trúc giải pháp

Nền tảng sử dụng kiến trúc bảo mật đa tầng của AWS trải rộng trên hai Availability Zones (AZs) để đảm bảo tính sẵn sàng cao:

![Kiến trúc SaaS HR Multi-Tenant](/images/5-Workshop/5.1-Overview/architecture.png)

#### Dịch vụ AWS sử dụng
- **Amazon CloudFront:** Mạng phân phối nội dung (CDN) toàn cầu đóng vai trò làm cổng biên bảo mật.
- **Amazon S3:** Lưu trữ giao diện tĩnh React SPA, chặn toàn bộ truy cập công cộng qua cơ chế Origin Access Control (OAC).
- **Amazon Cognito:** Quản lý đăng ký, đăng nhập và cấp phát token xác thực người dùng.
- **Application Load Balancer (ALB):** Định tuyến dựa trên đường dẫn API (`/api/v1/*`) đến các nhóm Target Groups tương ứng.
- **Amazon ECS (Fargate):** Chạy các microservices FastAPI (`auth`, `tenant`, và `hr`) dưới dạng container serverless.
- **Amazon RDS (MySQL):** Hệ quản trị cơ sở dữ liệu cấu hình Multi-AZ tự động chuyển vùng khi xảy ra sự cố.
- **Amazon SQS:** Hàng đợi tin nhắn xử lý bất đồng bộ, giảm tải cho các hoạt động ghi cơ sở dữ liệu.
- **AWS Secrets Manager:** Lưu trữ credentials cơ sở dữ liệu an toàn kết hợp hàm Lambda tự động xoay vòng mật khẩu.
- **Amazon CloudWatch & SNS:** Thu thập log hệ thống và gửi cảnh báo ngưỡng CPU/Memory qua email.

#### Thiết kế thành phần
- **Tầng trình diễn:** Người dùng kết nối qua CloudFront đến mã nguồn React tải từ S3.
- **Tầng ứng dụng:** Các microservices chạy trong private subnets của VPC, chỉ nhận dữ liệu chuyển tiếp từ ALB.
- **Tầng dữ liệu:** Cơ sở dữ liệu RDS MySQL nằm biệt lập trong các nhóm DB subnet riêng tư, chỉ chấp nhận kết nối từ tầng ứng dụng.
- **Tích hợp bất đồng bộ:** Hàng đợi SQS tách biệt hoạt động tạo tài khoản doanh nghiệp khỏi luồng API chính để tối ưu trải nghiệm người dùng.

---

### 4. Triển khai kỹ thuật

#### Các giai đoạn triển khai
- **Giai đoạn 1: Thiết kế kiến trúc & Dự toán chi phí (Tuần 1-2):** Vẽ sơ đồ luồng dữ liệu microservices và tính toán chi phí vận hành bằng AWS Pricing Calculator.
- **Giai đoạn 2: Khởi tạo hạ tầng mạng & Bảo mật (Tuần 3-5):** Xây dựng VPC đa subnet, thiết lập Security Groups và khởi tạo cơ sở dữ liệu RDS Multi-AZ.
- **Giai đoạn 3: Phát triển microservices & Đóng gói container (Tuần 6-8):** Đóng gói Docker cho các dịch vụ, đẩy lên ECR và cấu hình định tuyến ALB Target Groups.
- **Giai đoạn 4: CDN Frontend & Xoay vòng mật khẩu (Tuần 9-10):** Cấu hình CloudFront OAC tích hợp S3, deploy frontend React và lập trình xoay vòng Secrets Manager định kỳ.
- **Giai đoạn 5: Giám sát CloudWatch & Tối ưu chi phí FinOps (Tuần 11-12):** Thiết lập các cảnh báo ngưỡng hiệu năng CloudWatch, lên lịch tắt RDS ngoài giờ làm việc và chuyển đổi ECS sang Fargate Spot.

#### Yêu cầu kỹ thuật
- Thành thạo đóng gói ứng dụng Docker container.
- Sử dụng công cụ Terraform (IaC) để tự động hóa khởi tạo toàn bộ tài nguyên hạ tầng đám mây.
- Viết mã kịch bản Python Lambda xử lý việc xoay vòng mật khẩu định kỳ 30 ngày một lần.

---

### 5. Lộ trình & Mốc triển khai

- **Mốc 1 (Cuối Tháng 1):** Thiết lập hoàn chỉnh hạ tầng mạng VPC, Active Directory doanh nghiệp và cơ sở dữ liệu RDS MySQL trên AWS.
- **Mốc 2 (Cuối Tháng 2):** Đóng gói container thành công các microservices, định tuyến ALB hoàn chỉnh và triển khai tầng tính năng microservices.
- **Mốc 3 (Cuối Tháng 3):** Tích hợp CDN cho Frontend tĩnh, kích hoạt Secrets Manager xoay vòng mật khẩu, áp dụng tối ưu hóa chi phí FinOps và chạy kiểm thử E2E hệ thống.

---

### 6. Ước tính ngân sách

Ước tính chi phí chi tiết đã được cấu hình trên [AWS Pricing Calculator](https://calculator.aws/#/estimate?id=621f38b12a1ef026842ba2ddfe46ff936ed4ab01).

#### Chi phí hạ tầng hàng tháng (Đã tối ưu hóa FinOps)
- **ECS Fargate Compute (Chạy Spot):** $18.40/tháng
- **Amazon RDS MySQL (Multi-AZ db.t4g.micro):** $22.50/tháng
- **Application Load Balancer & Truyền nhận dữ liệu:** $8.30/tháng
- **CloudFront, S3, SSM & Cognito:** $2.50/tháng
- **Tổng ngân sách hàng tháng:** **$51.70 USD** (Tiết kiệm 61% chi phí vận hành so với cấu hình tiêu chuẩn $132.80 USD).

---

### 7. Đánh giá rủi ro

#### Ma trận rủi ro và giải pháp
- **Rò rỉ dữ liệu chéo giữa các Tenant:** Ảnh hưởng cao, xác suất thấp. Giải pháp: Ép buộc xác thực giải mã token JWT ở mọi API request để lấy đúng `tenant_id` trước khi truy vấn database.
- **Lộ thông tin đăng nhập Database:** Ảnh hưởng cao, xác suất thấp. Giải pháp: Tuyệt đối không hardcode mật khẩu; hệ thống tự động lấy mật khẩu động từ AWS Secrets Manager.
- **Vượt ngân sách dự toán:** Ảnh hưởng trung bình, xác suất thấp. Giải pháp: Cài đặt hạn mức cảnh báo ngân sách AWS Budgets và cảnh báo tài nguyên CloudWatch.

---

### 8. Kết quả mong đợi

- **Sẵn sàng thương mại hóa:** Hệ thống SaaS HR đa tổ chức an toàn, dễ bảo trì và khả năng tự động mở rộng theo lượng người dùng thực tế.
- **Mô hình bảo mật Zero-Trust:** Cô lập hoàn toàn tầng microservices và RDS trong mạng nội bộ, kết hợp lọc lưu lượng qua WAF và xoay vòng mật khẩu tự động.
- **Chi phí vận hành tối giản:** Tận dụng tối đa các công nghệ chia sẻ tài nguyên giúp giảm chi phí duy trì hệ thống đám mây xuống mức thấp nhất.