---
title: "Event 1"
date: 2026-05-23
weight: 1
chapter: false
pre: " <b> 4.1. </b> "
---

# Bài Thu Hoạch: "FCAJ Community Day – 23/5/2026"

---

## 1. Thông Tin Sự Kiện

|                    |                                         |
| ------------------ | --------------------------------------- |
| **Tên sự kiện**    | FCAJ Community Day                      |
| **Ngày tổ chức**   | 23/5/2026                               |
| **Đơn vị tổ chức** | First Cloud Journey (FCAJ)              |
| **Hình thức**      | Hội thảo trực tiếp + Workshop thực hành |

---

## 2. Mục Tiêu Sự Kiện

- Cập nhật kiến thức và xu hướng mới về AI và AWS
- Giới thiệu các dịch vụ AWS như **Amazon Q** và các ứng dụng thực tiễn trong doanh nghiệp
- Chia sẻ kinh nghiệm phát triển sản phẩm, tham gia hackathon và triển khai dự án thực tế
- Nâng cao hiểu biết về cách hoạt động của **mô hình ngôn ngữ lớn (LLM)** và hệ thống **Multi-Agent AI** trong môi trường doanh nghiệp

---

## 3. Danh Sách Diễn Giả

- **Tinh Truong** – Platform Engineer, GoTymeX
- **Anh Pham** – Cloud Consultant, G-AsiaPacific Vietnam
- **Thinh Nguyen** – DevOps Engineer, FCAJ
- **Team UTMorpho**:
  - **Uyen Le** – GenAI Engineer, VIB
  - **Thao Nguyen** – GenAI Engineer, VIB
  - **Mai Nguyen** – GenAI Engineer, VIB
- **Duc Dao** – Solutions Architect, Cloud Kinetics
- **Vy Lam** – Senior Business Systems Analyst, VPBank

---

## 4. Nội Dung Chính

### 4.1. Chia Sẻ Kiến Thức về AI & LLM

- Cập nhật xu hướng mới nhất về các mô hình ngôn ngữ lớn (LLM) và cách triển khai trong doanh nghiệp
- Giới thiệu **Amazon Q** – công cụ AI hỗ trợ toàn bộ vòng đời phát triển phần mềm (SDLC)
- Làm rõ vai trò của **Context**, **AI Memory** và **MCP (Model Context Protocol)** trong việc nâng cao hiệu quả hệ thống AI
- Hiểu rõ cơ chế suy luận (reasoning) của LLM và tính không ổn định trong quá trình sinh kết quả

### 4.2. Kiến Trúc Hệ Thống Multi-Agent

- Cách thiết kế và xây dựng **hệ thống Multi-Agent** để xử lý các bài toán phức tạp ở cấp độ doanh nghiệp
- Phối hợp nhiều AI agents để giải quyết các vấn đề mà một mô hình đơn lẻ không thể xử lý
- **Guardrails và Permission Boundaries**: Đảm bảo an toàn và kiểm soát truy cập trong hệ thống AI doanh nghiệp

### 4.3. Workshop Thực Hành

Người tham gia thực hành xây dựng hệ thống AI cấp doanh nghiệp qua 5 bài tập có cấu trúc:

1. **Add Authentication** – Triển khai Cognito/OAuth2 với xác thực JWT
2. **Implement Guardrails** – Cấu hình Bedrock Guardrails để lọc nội dung
3. **Permission Boundaries** – Thiết lập IAM với quyền truy cập tối thiểu cần thiết
4. **MCP Integration** – Tích hợp Model Context Protocol để kết nối công cụ
5. **Terraform Deployment** – Tạo Infrastructure as Code để triển khai nhất quán

### 4.4. Kinh Nghiệm Hackathon & Tư Duy Sản Phẩm

- Team UTMorpho xây dựng một sản phẩm hoàn chỉnh trong khoảng **18 tiếng**
- Các yếu tố then chốt: **quản lý thời gian**, **phân công rõ ràng** và **tận dụng công cụ AI** để tăng tốc phát triển
- Minh chứng rõ ràng rằng AI nên được xem là **công cụ tăng tốc**, không phải thay thế con người trong quy trình phát triển phần mềm

### 4.5. Định Hướng Nghề Nghiệp & Kinh Nghiệm Thực Chiến

- Kinh nghiệm thực chiến từ các kỹ sư đang làm việc tại các công ty Cloud/AI hàng đầu
- Kỹ năng cốt lõi cho kỹ sư Cloud/AI: tư duy sản phẩm, khả năng tự học và thích ứng nhanh
- Góc nhìn thực tế về thị trường việc làm và định hướng nghề nghiệp trong ngành công nghệ

---

## 5. Bài Học Chính

| Chủ đề                                                | Bài học                                                                                        |
| ----------------------------------------------------- | ---------------------------------------------------------------------------------------------- |
| **Context là chìa khóa**                              | Chất lượng đầu ra của LLM phụ thuộc rất nhiều vào cách thiết kế prompt và quản lý context      |
| **Bảo mật từ đầu**                                    | Tích hợp Guardrails và Permission Boundaries ngay từ khi thiết kế hệ thống AI                  |
| **MCP mở rộng khả năng**                              | Model Context Protocol giúp AI agents tương tác với bất kỳ công cụ hoặc hệ thống bên ngoài nào |
| **Tư duy sản phẩm quan trọng hơn kỹ thuật thuần túy** | Ưu tiên tính năng xoay quanh giá trị người dùng mới là yếu tố quyết định thành công            |
| **IaC là bắt buộc**                                   | Terraform cho phép triển khai hạ tầng AWS nhất quán và có thể tái tạo                          |

---

## 6. Ứng Dụng Vào Công Việc

- **Tích hợp MCP** vào workflow phát triển để kết nối AI agents với các công cụ và dịch vụ hiện có
- **Áp dụng Bedrock Guardrails**: Thiết lập lớp kiểm soát nội dung và an toàn cho hệ thống AI
- **Thực hành Terraform**: Xây dựng Infrastructure as Code cho các dự án triển khai trên AWS
- **Nghiên cứu thiết kế Multi-Agent**: Khám phá cách xây dựng hệ thống AI phức hợp cho bài toán thực tế
- **Áp dụng phương pháp Hackathon**: Rèn luyện tư duy phát triển nhanh và phối hợp nhóm hiệu quả

---

## 7. Cảm Nhận Cá Nhân

Tham gia **FCAJ Community Day 23/5/2026** là một trải nghiệm thực sự có giá trị, mang lại cái nhìn toàn diện và thực tế về AI và điện toán đám mây hiện đại. Đây không chỉ là một hội thảo kỹ thuật đơn thuần mà còn là không gian để trao đổi kiến thức, truyền cảm hứng và kết nối cộng đồng.

Workshop thực hành là điểm nhấn nổi bật nhất: thực hành trực tiếp các bài tập về Authentication, Guardrails, IAM, MCP và Terraform giúp tôi không chỉ hiểu _những gì_ các công nghệ này làm, mà còn hiểu _tại sao_ và _cách_ chúng kết hợp với nhau trong một hệ thống thực tế.

Câu chuyện hackathon – đặc biệt là Team UTMorpho xây dựng sản phẩm hoàn chỉnh trong 18 tiếng – thực sự truyền cảm hứng. Điều đó cho thấy trong thực tế, tốc độ thực thi và phối hợp nhóm quan trọng không kém gì chiều sâu kỹ thuật.

Giao lưu với các kỹ sư từ GoTymeX, Cloud Kinetics và VPBank cũng mang lại những góc nhìn thực tế, thiết thực về những kỹ năng thực sự quan trọng trên thị trường việc làm Cloud/AI hiện nay.

---

## 8. Hình Ảnh Sự Kiện

![Tham dự FCAJ Community Day cùng các bạn]({{< baseurl >}}images/event_1/event_1_1.jpg)

![Workshop exercises tại sự kiện – MCP Integration và Terraform Deployment]({{< baseurl >}}images/event_1/event_1_2.jpg)

> **Tổng thể**, FCAJ Community Day 23/5/2026 không chỉ cung cấp kiến thức kỹ thuật chuyên sâu về AI và AWS mà còn giúp tôi định hình rõ hơn tư duy phát triển sản phẩm, rèn luyện kỹ năng làm việc nhóm dưới áp lực và tiếp cận thực tiễn hơn với các công nghệ mới nhất trong ngành.
