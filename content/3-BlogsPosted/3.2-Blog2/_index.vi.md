---
title: "Giám sát hạ tầng chủ động sử dụng Ambient Agents trên Amazon Bedrock"
date: 2026-06-20
weight: 2
chapter: false
pre: " <b> 3.2. </b> "
---

# Chia sẻ giải pháp giám sát hạ tầng chủ động sử dụng Ambient Agents trên Amazon Bedrock

Trong quản lý hạ tầng điện toán đám mây quy mô lớn (Multi-Account/Multi-Region), việc xử lý số lượng lớn cảnh báo (Alert Fatigue) từ Amazon CloudWatch thường tiêu tốn nhiều thời gian của đội ngũ vận hành. Các hệ thống giám sát dựa trên quy tắc truyền thống đôi khi chỉ phát hiện khi sự cố đã xảy ra, gây khó khăn cho việc xâu chuỗi dữ liệu log và metric để xác định nguyên nhân gốc rễ (Root Cause Analysis).

Giải pháp **AgentWatch** cung cấp một mô hình **Ambient Agent** (Đại lý môi trường) hoạt động liên tục, hỗ trợ đội ngũ kỹ sư thu thập dữ liệu hạ tầng, phân tích hành vi hệ thống và đưa ra các đề xuất xử lý (Actionable Insights) nhằm tối ưu hóa quy trình vận hành.

---

## 1. Kiến trúc Vận hành & Cơ chế Phối hợp (Human-in-the-Loop)

AgentWatch được thiết kế để hoạt động song song với con người thông qua việc kết hợp giữa tự động hóa và quy trình phê duyệt nghiêm ngặt (Human-in-the-Loop - HITL), bao gồm hai luồng xử lý chính:

* **Giám sát tự động theo lịch trình (Scheduled Ambient Monitoring):** Được kích hoạt định kỳ mỗi 15 phút bởi Amazon EventBridge. Một tác vụ LangChain Agent tích hợp mô hình Claude trên Amazon Bedrock sẽ sử dụng các API chuyên dụng để truy vấn CloudWatch metrics, logs và alarms từ nhiều tài khoản AWS. Dữ liệu sau đó được LLM xử lý, trích xuất thông tin trọng tâm và gửi báo cáo về kênh Slack của đội ngũ.
* **Tương tác theo nhu cầu và kiểm soát HITL:** Kỹ sư có thể truy vấn trực tiếp với Agent theo thời gian thực qua Slack Slash Commands (ví dụ: `/ask Analyze log patterns for the last hour`). Hệ thống phân loại tác vụ dựa trên mức độ rủi ro: các tác vụ đọc thông tin hoặc phân tích xu hướng được xử lý tự động; trong khi các tác vụ thay đổi cấu hình hạ tầng nhạy cảm bắt buộc phải tuân theo 3 bước kiểm soát: Notify (Thông báo), Question (Làm rõ) và Review (Chờ phê duyệt từ con người).

![Slack Ambient Agent Architecture](/images/week10_agentwatch.png)

---

## 2. Các dịch vụ AWS cốt lõi trong kiến trúc

Giải pháp xây dựng một luồng công việc tự động hóa (Agentic Workflow) dựa trên sự phối hợp của các dịch vụ Cloud-Native:

* **Amazon Bedrock & Bedrock AgentCore Runtime:** Nền tảng cung cấp Foundation Model và môi trường runtime serverless bảo mật để vận hành các AI Agents ở quy mô doanh nghiệp.
* **Amazon EventBridge & AWS Lambda:** Đóng vai trò lập lịch và điều phối luồng công việc của Agent.
* **Amazon CloudWatch & AWS STS:** Cung cấp dữ liệu telemetry tập trung và cơ chế assume role phục vụ giám sát chéo tài khoản (Cross-Account Monitoring).
* **Amazon API Gateway & Amazon Cognito:** Đảm bảo kiểm soát truy cập và bảo mật (OAuth 2.0) cho các endpoint tiếp nhận webhook từ Slack.

---

## 3. Hiệu quả ứng dụng thực tế

* **Hỗ trợ phát hiện bất thường:** Khả năng xử lý ngôn ngữ tự nhiên (NLU) của LLM giúp liên kết các tín hiệu rời rạc từ log và metric hệ thống, hỗ trợ phát hiện các dấu hiệu bất thường mà cấu hình dựa trên quy tắc cố định có thể bỏ qua.
* **Hỗ trợ giảm thời gian xử lý sự cố (MTTR):** Agent tự động thực hiện các bước thu thập ngữ cảnh và phân tích ban đầu ngay khi phát hiện cảnh báo, cung cấp sẵn thông tin nền tảng giúp kỹ sư rút ngắn thời gian chẩn đoán.
* **Đảm bảo tính tuân thủ và an toàn (Governance):** Giảm bớt các thao tác thủ công lặp đi lặp lại của kỹ sư vận hành, đồng thời duy trì quyền kiểm soát của con người đối với môi trường Production thông qua các bước phê duyệt rõ ràng.

Giải pháp AgentWatch cho thấy tiềm năng ứng dụng của Generative AI (kiến trúc Agentic) trong việc tối ưu hóa hoạt động quản trị hạ tầng (Cloud Operations), chuyển đổi các hệ thống giám sát từ dạng hiển thị thông tin thụ động sang hỗ trợ phân tích dữ liệu chủ động hơn.

---

* **Link bài viết gốc:** [AgentWatch: Proactive AWS monitoring with ambient agents](https://aws.amazon.com/blogs/machine-learning/agentwatch-proactive-aws-monitoring-with-ambient-agents/)