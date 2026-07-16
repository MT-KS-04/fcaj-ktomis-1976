---
title: "Worklog Tuần 6"
date: 2026-06-08
weight: 6
chapter: false
pre: " <b> 6.1. </b> "
---

### Mục tiêu Tuần 6:

- Nắm được các cơ chế phân quyền nâng cao: Permission Boundaries, Policies & Conditions.
- Hiểu cách mã hóa dữ liệu với KMS và quản lý thông tin nhạy cảm với Secrets Manager.
- Biết cách bảo vệ ứng dụng web với AWS WAF và giám sát bảo mật với Security Hub.

### Các công việc thực hiện trong tuần:

| Ngày | Công việc                                                                                                                                                                                                                                                                  | Ngày bắt đầu | Ngày hoàn thành | Tài liệu tham khảo                 |
| ---- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------ | --------------- | ---------------------------------- |
| 2    | - Tìm hiểu IAM Permission Boundaries: <br>&emsp; + Khái niệm giới hạn quyền tối đa <br>&emsp; + Phân biệt boundary với identity-based policy <br> - **Thực hành:** <br>&emsp; + Gán permission boundary cho một IAM User                                                   | 08/06/2026   | 08/06/2026      | <https://000030.awsstudygroup.com> |
| 3    | - Tìm hiểu IAM Policies and Conditions: <br>&emsp; + Cấu trúc Effect, Action, Resource, Condition <br>&emsp; + Các condition key phổ biến (IP, MFA, tag) <br> - **Thực hành:** <br>&emsp; + Viết policy có điều kiện và kiểm tra hiệu lực                                  | 09/06/2026   | 09/06/2026      | <https://000044.awsstudygroup.com> |
| 4    | - Tìm hiểu AWS KMS: <br>&emsp; + Customer Master Key (CMK) <br>&emsp; + AWS managed key vs customer managed key <br>&emsp; + Envelope encryption <br> - **Thực hành:** <br>&emsp; + Mã hóa/giải mã dữ liệu <br>&emsp; + Bật mã hóa cho bucket S3                           | 10/06/2026   | 10/06/2026      | <https://000033.awsstudygroup.com> |
| 5    | - Tìm hiểu AWS Secrets Manager: <br>&emsp; + Lưu trữ thông tin nhạy cảm <br>&emsp; + Cơ chế rotation <br>&emsp; + So sánh với Parameter Store <br> - **Thực hành:** <br>&emsp; + Lưu và truy xuất secret bằng CLI <br>&emsp; + Phân biệt create-secret và put-secret-value | 11/06/2026   | 11/06/2026      | <https://000096.awsstudygroup.com> |
| 6    | - Tìm hiểu AWS WAF: <br>&emsp; + Web ACL, rule, rule group <br>&emsp; + Chặn SQL injection, XSS <br>&emsp; + Rate limit <br> - **Thực hành:** <br>&emsp; + Tạo Web ACL và gắn vào CloudFront/ALB                                                                           | 12/06/2026   | 12/06/2026      | <https://000026.awsstudygroup.com> |
| 7    | - Tìm hiểu AWS Security Hub: <br>&emsp; + Security standard <br>&emsp; + Finding và mức độ nghiêm trọng <br>&emsp; + Tích hợp với các dịch vụ bảo mật khác <br> - **Thực hành:** <br>&emsp; + Bật Security Hub và xem finding <br> - Tổng hợp kiến thức 6 tuần             | 13/06/2026   | 13/06/2026      | <https://000018.awsstudygroup.com> |

### Kết quả đạt được Tuần 6:

- Nắm được cơ chế phân quyền nâng cao với IAM Permission Boundaries:
  - Hiểu boundary chỉ giới hạn quyền tối đa, không tự cấp quyền
  - Phân biệt được boundary với identity-based policy
  - Áp dụng khi cần ủy quyền tạo IAM entity an toàn

- Kiểm soát truy cập chi tiết với IAM Policies and Conditions:
  - Nắm vững cấu trúc Effect, Action, Resource, Condition
  - Sử dụng các condition key phổ biến (IP, MFA, tag)
  - Viết được policy có điều kiện

- Hiểu và áp dụng được mã hóa với AWS KMS:
  - Khái niệm Customer Master Key
  - Phân biệt AWS managed key và customer managed key
  - Hiểu cơ chế envelope encryption (data key và master key)
  - Bật mã hóa cho dữ liệu trên S3

- Quản lý thông tin nhạy cảm an toàn với Secrets Manager:
  - Lưu trữ và truy xuất secret thay vì hardcode trong mã nguồn
  - Hiểu cơ chế rotation tự động
  - Phân biệt `create-secret` (tạo mới) và `put-secret-value` (cập nhật)
  - So sánh được với Parameter Store

- Bảo vệ ứng dụng web với AWS WAF:
  - Cấu hình Web ACL với các rule cơ bản
  - Chặn các tấn công phổ biến: SQL injection, XSS
  - Áp dụng rate limit

- Giám sát bảo mật tổng thể với AWS Security Hub:
  - Hiểu security standard và finding
  - Biết ưu tiên xử lý theo mức độ nghiêm trọng

- Nắm được bảo mật trên AWS là nhiều lớp: phân quyền, mã hóa, quản lý secret, bảo vệ ứng dụng và giám sát tổng thể.
- Hoàn thành giai đoạn học nền tảng, sẵn sàng bước vào giai đoạn triển khai dự án thực tế.
