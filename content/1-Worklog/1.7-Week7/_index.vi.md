---
title: "Worklog Tuần 7"
date: 2026-06-01
weight: 7
chapter: false
pre: " <b> 1.7. </b> "
---

**Week 7: Modernize the application**
**Name:** Lê Mạnh Cường
**ID:** 2280600340

### Week 7 Objectives:

* Kiến trúc Microservices: Phân rã dịch vụ và xác định giới hạn ngữ cảnh (bounded contexts).
* Điện toán Serverless: Xây dựng hệ thống hướng sự kiện (event-driven) và áp dụng mô hình ứng dụng trả tiền theo mức sử dụng (pay-per-use).
* Thiết kế API-First: Phát triển API theo tiêu chuẩn RESTful và GraphQL.
* Hệ thống Hướng sự kiện (Event-Driven): Áp dụng cơ chế nhắn tin bất đồng bộ (asynchronous messaging) và điều phối quy trình làm việc (workflow orchestration).
* Tích hợp DevOps: Xây dựng đường ống CI/CD và tự động hóa hạ tầng mạng.
* Hiện đại hóa Bảo mật: Thiết lập xác thực (Authentication), phân quyền (Authorization) và áp dụng các mô hình Zero-trust.

### Tasks to be carried out this week:

| Day | Task | Start Date | Completion Date | Reference Material |
| --- | --- | --- | --- | --- |
| 1 | - Di chuyển ứng dụng nguyên khối (Migrate Monolith) để chuẩn bị cho quá trình phân rã dịch vụ. <br> - Thiết lập tự động phát hành ứng dụng (Auto-release apps) thông qua việc xây dựng đường ống CI/CD và tự động hóa hạ tầng mạng. | 06/01/2026 | 06/01/2026 | <https://000050.awsstudygroup.com/> <br> <https://000051.awsstudygroup.com/> |
| 2 | - Tạo mới một Microservice bằng cách phân rã dịch vụ và xác định giới hạn ngữ cảnh (bounded contexts) cụ thể. <br> - Tái cấu trúc dữ liệu và quy trình làm việc (Data and workflow restructuring) cho phù hợp với hệ thống kiến trúc mới. | 06/02/2026 | 06/02/2026 | <https://000052.awsstudygroup.com/> <br> <https://000053.awsstudygroup.com/> |
| 3 | - Xây dựng hệ thống nhắn tin và định tuyến sự kiện cho Microservices, đồng thời áp dụng cơ chế nhắn tin bất đồng bộ (asynchronous messaging). <br> - Tạo và xác thực Ứng dụng Trang Đơn (Single Page Application - SPA) tuân thủ theo các mô hình bảo mật. | 06/03/2026 | 06/03/2026 | <https://000054.awsstudygroup.com/> <br> <https://000055.awsstudygroup.com/> |
| 4 | - Trải nghiệm các dịch vụ Trí tuệ Nhân tạo (AI services) trên nền tảng AWS. <br> - Bắt đầu làm quen và cấu hình AWS Step Functions để tiến hành điều phối quy trình làm việc (workflow orchestration). | 06/04/2026 | 06/04/2026 | <https://000047.awsstudygroup.com/> <br> <https://000056.awsstudygroup.com/> |
| 5 | - Cấu hình AWS Lambda tương tác với Amazon S3 và DynamoDB, áp dụng mô hình điện toán Serverless trả tiền theo mức sử dụng (pay-per-use). <br> - Xây dựng giao diện Frontend để gọi các dịch vụ qua API Gateway, áp dụng thiết kế API-First với tiêu chuẩn RESTful và GraphQL. | 06/05/2026 | 06/05/2026 | <https://000078.awsstudygroup.com/> <br> <https://000079.awsstudygroup.com/> |
| 6 | - Triển khai các ứng dụng Serverless bằng công cụ AWS SAM (Serverless Application Model). <br> - Tích hợp bảo mật với Amazon Cognito, tiến hành thiết lập xác thực (Authentication), phân quyền (Authorization) và áp dụng các mô hình Zero-trust. | 06/06/2026 | 06/06/2026 | <https://000080.awsstudygroup.com/> <br> <https://000081.awsstudygroup.com/> |

### Week 7 Achievements:

* **Module 50 & 51 (Migrate & CI/CD):** Thực hiện di chuyển ứng dụng nguyên khối (Migrate Monolith) và thiết lập tự động phát hành ứng dụng (Auto-release apps).
* **Module 52 & 53 (Microservices & Data):** Phân rã và tạo mới Microservice; tái cấu trúc dữ liệu và quy trình làm việc (workflow) tương thích với kiến trúc phân tán.
* **Module 54 & 55 (Messaging & SPA):** Xây dựng hệ thống nhắn tin, định tuyến sự kiện cho Microservices; tạo và xác thực thành công Ứng dụng Trang Đơn (SPA).
* **Module 47 & 56 (AI Services & Step Functions):** Trải nghiệm các dịch vụ AI trên AWS và cấu hình AWS Step Functions để điều phối quy trình làm việc.
* **Module 78 & 79 (Lambda & API Gateway):** Cấu hình AWS Lambda tương tác với S3/DynamoDB; xây dựng giao diện Frontend kết nối backend thông qua API Gateway.
* **Module 80 & 81 (AWS SAM & Cognito):** Triển khai ứng dụng Serverless bằng công cụ AWS SAM; thiết lập xác thực và bảo mật hệ thống thông qua Amazon Cognito.
