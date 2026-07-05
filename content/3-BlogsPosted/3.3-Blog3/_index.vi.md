---
title: "Tìm hiểu về VPC Link trong Private Integrations của Amazon API Gateway"
date: 2026-06-25
weight: 3
chapter: false
pre: " <b> 3.3. </b> "
---

# Chia sẻ về VPC Link trong tích hợp riêng tư (Private Integrations) của Amazon API Gateway

Trong việc thiết kế và xây dựng các hệ thống API có tính bảo mật cao, việc ẩn giấu các dịch vụ backend nằm bên trong mạng VPC riêng tư và không công khai ra ngoài Internet là một yêu cầu bắt buộc. **VPC Link** là một tài nguyên trong Amazon API Gateway cho phép kết nối các route của API đến các tài nguyên nội bộ, riêng tư này một cách an toàn.

Bài viết đi sâu vào các công nghệ cốt lõi đứng sau VPC Link (như AWS Hyperplane và AWS PrivateLink) và so sánh sự khác biệt cơ bản về mặt kiến trúc giữa VPC Link dành cho REST API và HTTP API.

---

## 1. Các công nghệ nền tảng

* **AWS Hyperplane:** Nền tảng ảo hóa mạng nội bộ hiệu năng cao của AWS, hỗ trợ kết nối và định tuyến giữa các VPC khác nhau. Hyperplane sử dụng cơ chế dịch địa chỉ mạng **VPC-to-VPC NAT** thay vì PrivateLink.
* **AWS PrivateLink:** Công nghệ cho phép truy cập các dịch vụ AWS một cách riêng tư trong mạng nội bộ của AWS mà không cần đi qua Internet công cộng. Traffic được dẫn qua các Interface VPC Endpoint (phía người dùng) và VPC Endpoint Service (phía nhà cung cấp).

---

## 2. Phân biệt Private API và Private Integration (Tích hợp riêng tư)

* **Private API:** Nghĩa là Endpoint của chính API Gateway chỉ có thể truy cập được từ bên trong VPC (hoặc qua Direct Connect/VPN). Hiện tại chỉ có REST API hỗ trợ cấu hình Private API.
* **Private Integration:** Nghĩa là hệ thống backend (phía sau API Gateway) nằm trong VPC và hoàn toàn không công khai ra Internet. API Gateway sử dụng VPC Link để kết nối tới backend này một cách an toàn.

---

## 3. So sánh VPC Link cho REST API vs. HTTP API

Điểm khác biệt đầu tiên nằm ở công nghệ nền tảng. VPC Link của REST API dựa trên **AWS PrivateLink**, trong khi HTTP API sử dụng hệ thống dịch mã địa chỉ mạng VPC-to-VPC NAT của **AWS Hyperplane**. Sự khác biệt này dẫn đến những thay đổi lớn về kiến trúc bên dưới:

* **Về tài nguyên và khả năng tích hợp:** HTTP API linh hoạt hơn hẳn khi không cần VPC Endpoint Service mà có thể kết nối trực tiếp đến ALB, NLB hoặc các dịch vụ đăng ký qua AWS Cloud Map; một VPC Link duy nhất cũng có thể liên kết với nhiều backend khác nhau. Ngược lại, REST API bắt buộc phải có VPC Endpoint Service, kết nối qua một NLB duy nhất và việc cấu hình đa backend phức tạp hơn nhiều.
* **Về tính năng và địa chỉ IP:** HTTP API tận dụng được sức mạnh Layer 7 của ALB (như định tuyến nâng cao, xác thực) và hoạt động theo cơ chế tạo tunnel bằng các ENI. Trong khi đó, REST API bị hạn chế hơn ở Layer 7 do đi qua NLB (Layer 4) và hệ thống backend phía sau sẽ nhận diện IP nguồn là IP riêng của chính NLB đó.

![VPC Link HTTP API Architecture](/images/week9_vpclink_http_alb.png)

---

## 4. Kết luận

Hiểu rõ sự khác biệt giữa hai loại VPC Link giúp các kỹ sư kiến trúc đưa ra quyết định chính xác khi thiết kế hệ thống:
* Nếu bạn cần một giải pháp API tiết kiệm chi phí, tốc độ cao hơn và tích hợp linh hoạt với ALB hoặc container, **VPC Link cho HTTP API** là sự lựa chọn tối ưu.
* Nếu bạn yêu cầu các tính năng chuyên sâu riêng biệt của REST API, bạn sẽ cần cấu hình **VPC Link qua cơ chế PrivateLink với NLB**.

---

* **Link bài viết gốc:** [Understanding VPC Links in Amazon API Gateway Private Integrations](https://aws.amazon.com/blogs/compute/understanding-vpc-links-in-amazon-api-gateway-private-integrations/)