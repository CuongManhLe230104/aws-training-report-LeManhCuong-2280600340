---
title: "Dọn dẹp"
date: 2024-07-08
weight: 11
chapter: false
pre: " <b> 5.11. </b> "
---

Xóa tài nguyên theo thứ tự ngược phụ thuộc để tránh phát sinh chi phí. **NAT Gateway, RDS và ALB tính tiền theo giờ** — xóa mấy cái này trước nếu chỉ muốn tạm dừng.

## Thứ tự dọn dẹp

1. **CloudFront** — disable, rồi xóa distribution.
2. **S3** — empty, rồi xóa `saashr-frontend-<acct>`.
3. **ALB** — xóa load balancer + 3 target group.
4. **ECS** — đặt service về desired 0, xóa các service, rồi xóa cluster.
5. **NAT Gateway** — xóa (chặn khoản tính giờ lớn nhất).
6. **RDS** — xóa database instance (bỏ qua hoặc lấy final snapshot).
7. **VPC endpoint** (nếu có) — xóa.
8. **Elastic IP** — release EIP của NAT.
9. **VPC** — xóa (kéo theo subnet, route table, IGW, security group).

Sau đó xóa các dịch vụ độc lập:
10. **SNS** topic + **CloudWatch** alarm + log group.
11. **ECR** repository (xóa image trước).
12. **Cognito** user pool, **SSM** parameter, **ACM** cert (nếu có dùng domain riêng).



{{% notice warning %}}
Kiểm tra lại trang **Billing → Budgets** sau một ngày để chắc chắn chi phí đã dừng. NAT Gateway và RDS còn sót là nguyên nhân hóa đơn bất ngờ thường gặp nhất.
{{% /notice %}}
