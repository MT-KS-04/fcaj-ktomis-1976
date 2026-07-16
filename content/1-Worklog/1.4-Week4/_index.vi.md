---
title: "Worklog Tuần 4"
date: 2026-05-25
weight: 4
chapter: false
pre: " <b> 4.1. </b> "
---

### Mục tiêu Tuần 4:

- Hiểu quy trình và công cụ di chuyển máy chủ, cơ sở dữ liệu lên AWS.
- Nắm được chiến lược khôi phục sau thảm họa (Disaster Recovery).
- Biết cách quản trị vận hành với Systems Manager và tổ chức tài nguyên bằng Tags.

### Các công việc thực hiện trong tuần:

| Ngày | Công việc                                                                                                                                                                                                                                                    | Ngày bắt đầu | Ngày hoàn thành | Tài liệu tham khảo                 |
| ---- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------ | --------------- | ---------------------------------- |
| 2    | - Tìm hiểu AWS VM Import/Export: <br>&emsp; + Các định dạng VM được hỗ trợ <br>&emsp; + Vai trò của S3 và IAM Role khi import <br>&emsp; + Quy trình import image thành AMI                                                                                  | 25/05/2026   | 25/05/2026      | <https://000014.awsstudygroup.com> |
| 3    | - Tìm hiểu AWS DMS và Schema Conversion Tool (SCT): <br>&emsp; + Homogeneous vs Heterogeneous migration <br>&emsp; + Full load và CDC (Change Data Capture) <br>&emsp; + Vai trò của SCT <br> - **Thực hành:** <br>&emsp; + Cấu hình replication task cơ bản | 26/05/2026   | 26/05/2026      | <https://000043.awsstudygroup.com> |
| 4    | - Tìm hiểu AWS Elastic Disaster Recovery: <br>&emsp; + Khái niệm RPO và RTO <br>&emsp; + Cơ chế replication liên tục <br>&emsp; + Quy trình failover / failback                                                                                              | 27/05/2026   | 27/05/2026      | <https://000100.awsstudygroup.com> |
| 5    | - Tìm hiểu AWS Systems Manager: <br>&emsp; + Parameter Store <br>&emsp; + Run Command <br>&emsp; + Patch Manager, Inventory <br> - **Thực hành:** <br>&emsp; + Quản lý EC2 instance qua Systems Manager <br>&emsp; + Lưu và đọc tham số với Parameter Store  | 28/05/2026   | 28/05/2026      | <https://000031.awsstudygroup.com> |
| 6    | - Tìm hiểu Systems Manager Session Manager: <br>&emsp; + Truy cập EC2 không cần SSH, không mở port 22 <br>&emsp; + Vai trò của IAM Role và SSM Agent <br> - **Thực hành:** <br>&emsp; + Mở phiên truy cập vào EC2 qua Session Manager                        | 29/05/2026   | 29/05/2026      | <https://000058.awsstudygroup.com> |
| 7    | - Tìm hiểu Tags và Resource Groups: <br>&emsp; + Tagging strategy <br>&emsp; + Vai trò của tag trong phân bổ chi phí <br> - **Thực hành:** <br>&emsp; + Gắn tag cho tài nguyên <br>&emsp; + Tạo Resource Group theo tag                                      | 30/05/2026   | 30/05/2026      | <https://000027.awsstudygroup.com> |

### Kết quả đạt được Tuần 4:

- Hiểu quy trình di chuyển máy chủ lên AWS với VM Import/Export:
  - Các định dạng VM được hỗ trợ
  - Vai trò của S3 và IAM Role trong quá trình import
  - Quy trình chuyển VM image thành AMI

- Nắm được cách di chuyển cơ sở dữ liệu với AWS DMS:
  - Phân biệt migration cùng loại và khác loại
  - Vai trò của Schema Conversion Tool khi đổi engine
  - Hiểu full load và CDC giúp giảm downtime khi di chuyển

- Nắm được chiến lược khôi phục sau thảm họa với Elastic Disaster Recovery:
  - Phân biệt RPO (mức mất mát dữ liệu tối đa) và RTO (thời gian phục hồi)
  - Cơ chế replication liên tục
  - Quy trình failover và failback

- Biết cách quản trị tập trung với AWS Systems Manager:
  - Lưu cấu hình với Parameter Store (String và SecureString)
  - Thực thi lệnh từ xa với Run Command
  - Vá lỗi và kiểm kê với Patch Manager, Inventory

- Truy cập máy chủ an toàn với Session Manager:
  - Không cần key pair, không cần mở port 22
  - Hiểu điều kiện cần: IAM Role `AmazonSSMManagedInstanceCore` và SSM Agent
  - So sánh được ưu điểm bảo mật so với SSH truyền thống

- Tổ chức tài nguyên hiệu quả với Tags và Resource Groups:
  - Xây dựng tagging strategy nhất quán
  - Nhóm tài nguyên theo tag
  - Dùng tag để phân bổ chi phí
