---
title: "Worklog Tuần 6"
date: 2026-06-08
weight: 6
chapter: false
pre: " <b> 6.1. </b> "
---

## Thông tin chung

| Nội dung         | Chi tiết                                                                                          |
| ---------------- | ------------------------------------------------------------------------------------------------- |
| Thời gian        | 08/06/2026 - 14/06/2026                                                                           |
| Tuần thực tập    | Tuần 6                                                                                            |
| Giai đoạn        | Optimize - Security                                                                               |
| Chương trình học | First Cloud Journey                                                                               |
| Chủ đề chính     | Bảo mật: phân quyền nâng cao, mã hóa, quản lý secret, bảo vệ ứng dụng                             |
| Mục tiêu tuần    | Nắm IAM Permission Boundaries, IAM Policies & Conditions, KMS, Secrets Manager, WAF, Security Hub |

## Định hướng học tập Tuần 6

Tuần 6 tập trung vào nhóm **Security** trong giai đoạn **Optimize**. Nội dung gồm phân quyền nâng cao (Permission Boundaries, IAM Policies and Conditions), mã hóa (KMS), quản lý thông tin nhạy cảm (Secrets Manager), bảo vệ ứng dụng (WAF) và tổng hợp trạng thái bảo mật (Security Hub). Em học từ phần gần với IAM đã biết trước, rồi tiến dần sang mã hóa và bảo vệ ứng dụng, mỗi ngày 1–2 chủ đề.

## Mục tiêu học tập Tuần 6

- Tìm hiểu Permission Management with IAM Permission Boundaries.
- Tìm hiểu Access Control with IAM Policies and Conditions.
- Tìm hiểu Encryption with AWS Key Management Service (KMS).
- Tìm hiểu Credentials Management with AWS Secrets Manager.
- Tìm hiểu Application Protection with AWS WAF.
- Tìm hiểu Security Compliance with AWS Security Hub.

## Nội dung thực hiện trong tuần

### Ngày 1 - Thứ hai, 08/06/2026

Chủ đề: **Permission Management with IAM Permission Boundaries**.

Nội dung đã thực hiện:

- Đọc về Permission Boundary và ý nghĩa "giới hạn quyền tối đa" của một IAM entity.
- Phân biệt boundary với identity-based policy.
- Làm theo hướng dẫn gán thử một permission boundary cho một IAM User.

Kết quả đạt được:

- Hiểu boundary khác policy thường ở chỗ nào.
- Gán được boundary cho một entity theo ví dụ.

### Ngày 2 - Thứ ba, 09/06/2026

Chủ đề: **Access Control with IAM Policies and Conditions**.

Nội dung đã thực hiện:

- Đọc kỹ hơn cấu trúc policy: Effect, Action, Resource và đặc biệt là Condition.
- Tìm hiểu vài condition key hay dùng (IP, MFA, tag).
- Viết thử một policy có điều kiện rồi kiểm tra xem nó chặn đúng như mong đợi không.

Kết quả đạt được:

- Hiểu Condition cho phép kiểm soát truy cập chi tiết tới mức nào.
- Viết được một policy có điều kiện đơn giản.

### Ngày 3 - Thứ tư, 10/06/2026

Chủ đề: **Encryption with AWS Key Management Service (KMS)**.

Nội dung đã thực hiện:

- Đọc về KMS: khái niệm CMK, phân biệt AWS managed key và customer managed key.
- Tìm hiểu envelope encryption.
- Làm theo hướng dẫn thử mã hóa/giải mã dữ liệu và bật mã hóa cho một bucket S3.

Kết quả đạt được:

- Hiểu KMS quản lý khóa và mã hóa dữ liệu thế nào.
- Bật được mã hóa cho S3 theo hướng dẫn.

### Ngày 4 - Thứ năm, 11/06/2026

Chủ đề: **Credentials Management with AWS Secrets Manager**.

Nội dung đã thực hiện:

- Đọc về Secrets Manager và cơ chế tự luân chuyển (rotation) secret.
- So sánh Secrets Manager với Parameter Store đã học ở tuần 4.
- Làm thử: lưu một secret (ví dụ thông tin kết nối database) rồi truy xuất lại.

Lưu một secret rồi đọc lại bằng CLI:

```bash
aws secretsmanager create-secret --name intern/db-cred \
  --secret-string '{"username":"admin","password":"P@ss123"}'

aws secretsmanager get-secret-value --secret-id intern/db-cred \
  --query "SecretString" --output text
```

```json
{ "username": "admin", "password": "P@ss123" }
```

Em có thử tạo lại secret trùng tên thì bị:

```
An error occurred (ResourceExistsException): The operation failed because the secret intern/db-cred already exists.
```

Muốn cập nhật giá trị thì phải dùng `put-secret-value` chứ không phải `create-secret` — đây là chỗ em nhầm.

Kết quả đạt được:

- Hiểu Secrets Manager giúp quản lý credential an toàn hơn là để trong code.
- Lưu và đọc được một secret cơ bản.
- Phân biệt được `create-secret` (tạo mới) và `put-secret-value` (cập nhật).

### Ngày 5 - Thứ sáu, 12/06/2026

Chủ đề: **Application Protection with AWS WAF**.

Nội dung đã thực hiện:

- Đọc về WAF và cách nó chặn các tấn công web phổ biến (SQL injection, XSS, rate limit).
- Tìm hiểu Web ACL, rule và rule group.
- Làm theo hướng dẫn tạo một Web ACL với rule cơ bản và gắn thử vào CloudFront/ALB.

Kết quả đạt được:

- Hiểu WAF bảo vệ ứng dụng web ở lớp nào.
- Cấu hình được một Web ACL đơn giản.

### Ngày 6 - Thứ bảy, 13/06/2026

Chủ đề: **Security Compliance with AWS Security Hub**.

Nội dung đã thực hiện:

- Đọc về Security Hub và cách nó gom trạng thái bảo mật về một chỗ.
- Tìm hiểu security standard và finding.
- Bật thử Security Hub và xem qua các finding nó báo về.
- Tổng hợp kiến thức cả tuần và cả 6 tuần.

Kết quả đạt được:

- Hiểu Security Hub cho cái nhìn tổng thể về bảo mật.
- Đọc được các finding và biết ưu tiên theo mức độ nghiêm trọng.

## Tổng kết kiến thức Tuần 6

| Nhóm kiến thức       | Nội dung đã học                              |
| -------------------- | -------------------------------------------- |
| Permission           | IAM Permission Boundaries                    |
| Access Control       | IAM Policies and Conditions                  |
| Encryption           | KMS, CMK, envelope encryption                |
| Secrets              | Secrets Manager, rotation                    |
| Application Security | AWS WAF, Web ACL, rule                       |
| Compliance           | AWS Security Hub, security standard, finding |

## Kết quả đạt được trong tuần

- Hiểu và gán thử được permission boundary, viết policy có condition.
- Bật được mã hóa dữ liệu bằng KMS.
- Lưu và quản lý được secret với Secrets Manager.
- Cấu hình được WAF bảo vệ ứng dụng web.
- Bật và đọc được finding trong Security Hub.

## Khó khăn gặp phải

- Permission boundary với policy thường lúc đầu em cứ tưởng là một, đọc kỹ mới hiểu boundary chỉ giới hạn quyền tối đa chứ không tự cấp quyền.
- Condition trong policy nhiều key quá, em không nhớ hết được, đành làm quen dần từ mấy cái đơn giản như IP với MFA.
- Envelope encryption đọc chữ thì thấy trừu tượng, em phải vẽ ra data key với master key mới hình dung được nó lồng nhau thế nào.

## Bài học rút ra

- Học xong tuần này em thấy bảo mật không nằm ở một chỗ, mà rải ra nhiều lớp: phân quyền, mã hóa, bảo vệ ứng dụng rồi giám sát tổng thể.
- Chuyện để mật khẩu hay key trong code là thói quen xấu, có Secrets Manager rồi thì nên bỏ hẳn.
- Security Hub tiện ở chỗ gom hết về một màn hình, nhưng finding nhiều nên phải biết ưu tiên chứ không ôm hết một lúc.

## Tổng kết 6 tuần

Qua 6 tuần, em đã đi gần hết các phần chính của First Cloud Journey: **Explore AWS Services** (tuần 1–3), **Migrate to AWS** và bước đầu **Optimize** (tuần 4), tiếp tục **Optimize - Operations & Cost** (tuần 5) và **Optimize - Security** (tuần 6). Từ chỗ chưa biết gì, giờ em đã có cái nền tương đối về tài khoản, mạng, tính toán, lưu trữ, database, rồi migration, IaC, chi phí và bảo mật.

## Nhận xét cuối tuần

Tuần 6 khép lại 6 tuần đầu bằng nhóm chủ đề bảo mật, cũng là nhóm em thấy cần đọc chậm và cẩn thận nhất. Nhìn lại cả chặng, cách học đi từ dễ tới khó và mỗi ngày chỉ 1–2 dịch vụ giúp em không bị ngợp, hiểu tới đâu chắc tới đó thay vì học vội cho xong.
