---
title: "Week 9 Worklog"
date: 2026-06-15
weight: 9
chapter: false
pre: " <b> 1.9. </b> "
---

**BÁO CÁO KỸ THUẬT: ĐÁNH GIÁ KIẾN TRÚC MẠNG BẢO MẬT VÀ QUẢN LÝ THÔNG TIN XÁC THỰC TRÊN AWS**
**Name:** Lê Mạnh Cường
**ID:** 2280600340

### Week 9 Objectives:

* Phân hệ Bảo mật & Dữ liệu: Khảo sát cơ chế bảo vệ thông tin xác thực chặng cuối (last-mile credentials). Thiết lập luồng gọi API động từ AWS Lambda đến AWS Secrets Manager để truy vấn cơ sở dữ liệu Amazon RDS (MySQL) mà không làm lộ cấu hình mã nguồn.
* Phân hệ Tích hợp Mạng riêng tư: Tìm hiểu nguyên lý hoạt động và công nghệ nền tảng của VPC Link trên Amazon API Gateway. Đánh giá sự khác biệt về mặt kiến trúc hệ thống mạng giữa hai mô hình REST API và HTTP API.

### Tasks to be carried out this week:

| Day | Task | Start Date | Completion Date | Reference Material |
| --- | --- | --- | --- | --- |
| 1 | - Phân tích giải pháp bảo mật credentials cho hệ thống dữ liệu: Khảo sát các rủi ro khi lưu cứng (hardcode) mật khẩu ứng dụng. <br> - Thiết lập quy trình kết nối an toàn bảo vệ cơ sở dữ liệu backend: Client → API Gateway → AWS Lambda → Gọi Secrets Manager lấy cấu hình. | 06/15/2026 | 06/15/2026 | <https://aws.amazon.com/vi/blogs/compute/understanding-vpc-links-in-amazon-api-gateway-private-integrations/> |
| 2 | - Nghiên cứu tự động hóa cấu hình qua CloudFormation: Tìm hiểu cách sử dụng AWS CloudFormation template để tự động hóa khởi tạo cụm tài nguyên bao gồm RDS MySQL, API Gateway và các hàm Lambda. | 06/16/2026 | 06/16/2026 | <https://aws.amazon.com/vi/blogs/security/how-to-securely-provide-database-credentials-to-lambda-functions-by-using-aws-secrets-manager/> |
| 3 | - Nghiên cứu cơ chế Tham chiếu động & Tự động xoay vòng: Áp dụng Dynamic References để lấy mật khẩu từ Secrets Manager khi tạo RDS, tránh ghi log văn bản thuần (plain text). <br> - Cấu hình tài nguyên `AWS::SecretsManager::RotationSchedule` phối hợp hàm Lambda phụ trách tự động reset mật khẩu sau mỗi 30 ngày. | 06/17/2026 | 06/17/2026 | |
| 4 | - Phân biệt bản chất Private API và Private Integration: Định nghĩa rạch ròi hệ thống: Private API giới hạn endpoint của chính API Gateway trong VPC (chỉ REST API hỗ trợ); Private Integration bảo vệ backend ẩn trong VPC thông qua cổng kết nối VPC Link. | 06/18/2026 | 06/18/2026 | |
| 5 | - Đánh giá hạ tầng VPC Link cho dòng REST API: Nghiên cứu công nghệ nền tảng dựa trên AWS PrivateLink. <br> - Xác định ràng buộc: Bắt buộc phải cấu hình qua VPC Endpoint Service, kết nối tới một NLB (Layer 4) duy nhất và nhận diện IP nguồn từ chính NLB đó. | 06/19/2026 | 06/19/2026 | |
| 6 | - Đánh giá hạ tầng VPC Link cho dòng HTTP API: Nghiên cứu công nghệ nền tảng dựa trên cơ chế VPC-to-VPC NAT của hệ thống ảo hóa mạng AWS Hyperplane. <br> - Xác định ưu điểm: Kết nối trực tiếp qua các "đường hầm" ENI đến đa backend (ALB, NLB, Cloud Map), tận dụng sức mạnh định tuyến Layer 7 của ALB. | 06/20/2026 | 06/20/2026 | |
| 7 | - Tổng hợp, đối sánh và xây dựng báo cáo kiến trúc: Tiến hành so sánh, đối chiếu ưu - nhược điểm về chi phí và hiệu năng của hai loại VPC Link. <br> - Chuẩn hóa toàn bộ sơ đồ kiến trúc hệ thống và đóng gói tài liệu báo cáo tiến độ tuần. | 06/21/2026 | 06/21/2026 | |

### Week 9 Achievements:

* Đã hoàn thành phân tích và thiết lập quy trình kết nối an toàn bảo vệ cơ sở dữ liệu backend, loại bỏ rủi ro lưu cứng mật khẩu.
* Nghiên cứu thành công việc tự động hóa cấu hình hạ tầng (RDS, API Gateway, Lambda) qua AWS CloudFormation.
* Áp dụng thành công cơ chế Tham chiếu động (Dynamic References) và tự động xoay vòng mật khẩu (RotationSchedule) mỗi 30 ngày qua Secrets Manager.
  ![AWS Secrets Manager Database Rotation](images/week9_secretsmanager.png)
* Phân biệt và định nghĩa rõ ràng bản chất kiến trúc giữa Private API và Private Integration.
* Hoàn tất đánh giá hạ tầng VPC Link cho cả dòng REST API (dựa trên AWS PrivateLink) và HTTP API (dựa trên AWS Hyperplane).
  * **Kiến trúc REST API VPC Link:**
    ![REST API VPC Link Architecture](images/week9_vpclink_rest.png)
  * **Kiến trúc HTTP API VPC Link (NLB):**
    ![HTTP API VPC Link NLB Architecture](images/week9_vpclink_http_nlb.png)
  * **Kiến trúc HTTP API VPC Link (Hyperplane/ALB):**
    ![HTTP API VPC Link Hyperplane ALB Architecture](images/week9_vpclink_http_alb.png)
* Xây dựng báo cáo kiến trúc hoàn chỉnh, so sánh chi tiết ưu - nhược điểm của các loại VPC Link.