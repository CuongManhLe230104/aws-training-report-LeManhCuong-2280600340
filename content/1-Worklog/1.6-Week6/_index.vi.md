---
title: "Worklog Tuần 6"
date: 2026-05-25
weight: 6
chapter: false
pre: " <b> 1.6. </b> "
---

**Phát triển các API mở rộng & phân quyền cho hệ thống SaaS HR Multi-tenant**
**Name:** Lê Mạnh Cường
**ID:** 2280600340

### Week 6 Objectives:

* Dịch vụ Xác thực (auth-service): Thiết kế và xây dựng các API quản trị thành viên trong doanh nghiệp (Workspace Users), phân quyền vai trò (Owner, Admin, Member) và quản lý quyền truy cập.
* Dịch vụ Nhân sự (hr-service): Phát triển API cập nhật hồ sơ/chức vụ nhân viên và API xóa nhân viên ra khỏi hệ thống của tenant, đảm bảo ràng buộc an toàn dữ liệu.
* Dịch vụ Doanh nghiệp (tenant-service): Phát triển API tự xem thông tin doanh nghiệp (dành cho nhân viên thuộc tenant) và cập nhật thông tin cơ bản (logo, tên doanh nghiệp) cho Owner.

### Tasks to be carried out this week:

| Day | Task | Start Date | Completion Date | Reference Material |
| --- | --- | --- | --- | --- |
| 1 | Phân tích & thiết kế cơ sở dữ liệu cho Auth Service: <br> - Khảo sát bảng users và user_tenants hiện có. <br> - Thiết kế đặc tả các API quản lý Workspace Users: Liệt kê người dùng thuộc tenant hiện tại, cập nhật vai trò, và trục xuất thành viên. | 05/25/2026 | 05/25/2026 | |
| 2 | Đặc tả logic và hiện thực Auth Service APIs: <br> - Xây dựng các hàm CRUD truy vấn dữ liệu từ bảng user_tenants. <br> - Xây dựng router xử lý, tích hợp middleware kiểm tra quyền hạn (chỉ Owner hoặc Admin mới được phép sửa đổi vai trò hoặc trục xuất người dùng khỏi tenant). | 05/26/2026 | 05/26/2026 | |
| 3 | Phân tích & thiết kế API cập nhật/xóa nhân viên cho HR Service: <br> - Khảo sát các trường dữ liệu cần cập nhật trong hồ sơ nhân viên (EmployeeUpdate). <br> - Thiết kế các endpoint cập nhật và xóa. <br> - Thiết kế ràng buộc bảo mật: Chỉ cho phép tài khoản có vai trò 'admin' hoặc 'owner' thực hiện thay đổi thông tin nhân viên hoặc xóa nhân viên. | 05/27/2026 | 05/27/2026 | |
| 4 | Đặc tả logic và hiện thực HR Service APIs: <br> - Viết các hàm CRUD để cập nhật hồ sơ (update_employee) và xóa nhân viên (delete_employee). <br> - Cài đặt các API endpoints trong router hr.py. <br> - Thực hiện trích xuất tenant_id từ JWT token để bảo đảm tính cô lập thông tin nhân sự giữa các tenant. | 05/28/2026 | 05/28/2026 | |
| 5 | Phân tích & thiết kế các API quản trị cấu hình Tenant: <br> - Thiết kế API xem cấu hình doanh nghiệp và API cập nhật logo/tên doanh nghiệp. <br> - Xác định cấu trúc Tenant DB hiện tại và xác định luồng dữ liệu truyền tải giữa Client và Tenant Service. | 05/29/2026 | 05/29/2026 | |
| 6 | Đặc tả logic và hiện thực Tenant Service APIs: <br> - Triển khai router tenants.py để xử lý yêu cầu xem và cập nhật cấu hình. <br> - Sử dụng tenant_id lấy từ token xác thực của người dùng gửi lên để xác định chính xác doanh nghiệp cần truy vấn, tránh rò rỉ dữ liệu hoặc cập nhật trái phép chéo giữa các tenant. | 05/30/2026 | 05/30/2026 | |
| 7 | Kiểm tra tổng thể các API mới phát triển: <br> - Xây dựng bộ testcase bằng Postman / cURL để mô phỏng luồng gọi API thông qua Nginx API Gateway. <br> - Kiểm tra phân quyền (Role-based Access Control - RBAC) và tính cô lập dữ liệu (Multi-tenancy). <br> - Dọn dẹp dữ liệu thử nghiệm và chuẩn bị môi trường chạy thật. | 05/31/2026 | 05/31/2026 | |

### Week 6 Achievements:

* Thiết kế và xây dựng thành công các API quản trị thành viên trong doanh nghiệp, phân quyền vai trò (Owner, Admin, Member) và quản lý quyền truy cập cho Dịch vụ Xác thực (auth-service).
  ![SaaS HR Auth Service API](images/auth_service_1.png)
* Phát triển hoàn thiện API cập nhật hồ sơ/chức vụ và xóa nhân viên cho Dịch vụ Nhân sự (hr-service), tích hợp thành công trích xuất `tenant_id` từ JWT token để đảm bảo tính cô lập dữ liệu.
  ![SaaS HR Core Service API](images/core_service.png)
* Hoàn thành phát triển API cho Dịch vụ Doanh nghiệp (tenant-service) giúp xem và cập nhật cấu hình doanh nghiệp một cách bảo mật.
  ![SaaS HR Tenant Service API](images/tenant_service.png)
* Kiểm tra thành công toàn bộ hệ thống API thông qua Nginx API Gateway, xác minh hệ thống phân quyền (RBAC) và cô lập dữ liệu Multi-tenancy hoạt động chính xác.
