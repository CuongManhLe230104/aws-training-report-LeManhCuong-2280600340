---
title: "Bảo mật database credentials cho AWS Lambda với AWS Secrets Manager"
date: 2026-06-15
weight: 1
chapter: false
pre: " <b> 3.1. </b> "
---

# Sử dụng AWS Secrets Manager bảo mật database credentials cho AWS Lambda

Trong quá trình phát triển các ứng dụng Serverless, một trong những thách thức lớn nhất là làm thế nào để lưu trữ và truyền thông tin xác thực cơ sở dữ liệu (credentials) đến các hàm AWS Lambda một cách an toàn. Việc lưu trữ trực tiếp (hardcode) mật khẩu trong mã nguồn hoặc truyền qua biến môi trường (Environment Variables) luôn tiềm ẩn rủi ro rò rỉ thông tin nhạy cảm.

Giải pháp sử dụng **AWS Secrets Manager** giúp loại bỏ hoàn toàn các rủi ro trên bằng cách lưu trữ tập trung thông tin xác thực và cho phép các hàm Lambda truy vấn động khi kết nối với Amazon RDS (MySQL).

---

## 1. Mô hình hoạt động của giải pháp

Quy trình xử lý yêu cầu kết nối an toàn từ Client đến cơ sở dữ liệu Backend được mô tả qua các bước sau:

1. **Client** gửi Request đến RESTful API được lưu trữ trên **AWS API Gateway**.
2. **API Gateway** thực thi hàm **AWS Lambda** tương ứng.
3. Hàm **Lambda** gọi API của **AWS Secrets Manager** để lấy thông tin đăng nhập cơ sở dữ liệu (username/password).
4. Hàm **Lambda** sử dụng thông tin đó để kết nối, truy vấn cơ sở dữ liệu **Amazon RDS (MySQL)** và trả lại kết quả.

![AWS Secrets Manager Database Rotation](/images/week9_secretsmanager.png)

---

## 2. Quy trình triển khai thông qua CloudFormation

Để tự động hóa và quản lý hạ tầng dưới dạng mã (IaC), bài viết cung cấp một template AWS CloudFormation để khởi tạo nhanh cụm tài nguyên bao gồm:

* Một cơ sở dữ liệu **Amazon RDS MySQL** (loại instance `db.t3.micro`).
* Hai hàm **Lambda**:
  * `LambdaRDSCFNInit`: Dùng để khởi tạo bảng `Employees` và thêm dữ liệu mẫu ngay sau khi khởi tạo stack.
  * `LambdaRDSTest`: Dùng để truy vấn đếm số lượng nhân viên thực tế phục vụ kiểm thử.
* Một **RESTful API Gateway** với phương thức `GET`.
* Một tài nguyên **Secret** trong Secrets Manager chứa mật khẩu được tạo ngẫu nhiên.

---

## 3. Các điểm cốt lõi về mặt kỹ thuật

* **Tham chiếu động (Dynamic References):** CloudFormation sử dụng tính năng tham chiếu động để lấy mật khẩu trực tiếp từ Secrets Manager khi tạo RDS instance. Điều này đảm bảo mật khẩu không bao giờ được ghi log hay lưu lại dưới dạng văn bản thuần túy (plain text) trong các file cấu hình.
* **Tự động xoay vòng mật khẩu (Automatic Rotation):** Cấu hình tài nguyên `AWS::SecretsManager::RotationSchedule` phối hợp với một hàm Lambda xoay vòng để tự động thay đổi mật khẩu cơ sở dữ liệu RDS định kỳ sau mỗi **30 ngày**, giảm thiểu tối đa rủi ro khi mật khẩu bị rò rỉ.

Việc kết hợp Lambda với AWS Secrets Manager giúp doanh nghiệp quản lý vòng đời của các thông tin nhạy cảm một cách tự động, giảm chi phí vận hành hạ tầng bảo mật riêng, và nâng cao đáng kể mức độ an toàn cho các ứng dụng Serverless.

---

* **Link bài viết gốc:** [How to securely provide database credentials to Lambda functions by using AWS Secrets Manager](https://aws.amazon.com/blogs/security/how-to-securely-provide-database-credentials-to-lambda-functions-by-using-aws-secrets-manager/)