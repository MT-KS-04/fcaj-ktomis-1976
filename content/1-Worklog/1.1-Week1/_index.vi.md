---
title: "Worklog Tuần 1"
date: 2026-05-05
weight: 1
chapter: false
pre: " <b> 1.1. </b> "
---

### Mục tiêu Tuần 1:

- Làm quen và kết nối với các thành viên trong First Cloud AI Journey.
- Tạo và bảo mật tài khoản AWS, nắm được cách quản lý chi phí.
- Hiểu các dịch vụ AWS nền tảng: IAM, VPC, EC2, S3 và cách dùng Console & CLI.

### Các công việc thực hiện trong tuần:

| Ngày | Công việc                                                                                                                                                                                                                                                                                                                                            | Ngày bắt đầu | Ngày hoàn thành | Tài liệu tham khảo                                                                                                 |
| ---- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------ | --------------- | ------------------------------------------------------------------------------------------------------------------ |
| 3    | - Làm quen với các thành viên FCAJ <br> - Đọc và ghi chú nội quy, quy định tại đơn vị thực tập <br> - Xem tổng quan lộ trình học First Cloud Journey                                                                                                                                                                                                 | 05/05/2026   | 05/05/2026      | <https://cloudjourney.awsstudygroup.com/1-explore/>                                                                |
| 4    | - Tìm hiểu điện toán đám mây và các nhóm dịch vụ AWS <br>&emsp; + Compute <br>&emsp; + Storage <br>&emsp; + Networking <br>&emsp; + Database <br>&emsp; + ... <br> - **Thực hành:** <br>&emsp; + Tạo tài khoản AWS Free Tier <br>&emsp; + Bật MFA cho root account <br>&emsp; + Thiết lập AWS Budgets cảnh báo chi phí                               | 06/05/2026   | 06/05/2026      | <https://000001.awsstudygroup.com> <br> <https://000007.awsstudygroup.com>                                         |
| 5    | - Tìm hiểu AWS Support và cách tạo support case <br> - Tìm hiểu AWS IAM: <br>&emsp; + User, Group <br>&emsp; + Role, Policy <br>&emsp; + Nguyên tắc least privilege <br> - **Thực hành:** <br>&emsp; + Tạo IAM User với quyền hạn chế <br>&emsp; + Đọc cấu trúc IAM Policy dạng JSON                                                                 | 07/05/2026   | 07/05/2026      | <https://000009.awsstudygroup.com> <br> <https://000002.awsstudygroup.com>                                         |
| 6    | - Tìm hiểu Amazon VPC: <br>&emsp; + CIDR block, Subnet <br>&emsp; + Route Table, Internet Gateway, NAT Gateway <br>&emsp; + Security Group vs Network ACL <br> - **Thực hành:** <br>&emsp; + Dựng VPC có public và private subnet                                                                                                                    | 08/05/2026   | 08/05/2026      | <https://000003.awsstudygroup.com>                                                                                 |
| 7    | - Tìm hiểu Amazon EC2: <br>&emsp; + Instance types, AMI <br>&emsp; + Key pair, EBS volume <br> - Tìm hiểu IAM Roles for EC2 (instance profile) <br> - **Thực hành:** <br>&emsp; + Khởi tạo EC2 instance Free Tier <br>&emsp; + Kết nối SSH vào instance <br>&emsp; + Cài đặt & cấu hình AWS CLI <br>&emsp; + Dùng lệnh `aws sts get-caller-identity` | 09/05/2026   | 09/05/2026      | <https://000004.awsstudygroup.com> <br> <https://000048.awsstudygroup.com> <br> <https://000011.awsstudygroup.com> |
| CN   | - Tìm hiểu Amazon S3: <br>&emsp; + Bucket, Object, Storage class <br>&emsp; + Bucket policy, Block Public Access <br> - **Thực hành:** <br>&emsp; + Tạo bucket và upload file <br>&emsp; + Bật static website hosting <br>&emsp; + Cấu hình bucket policy cho phép truy cập công khai                                                                | 10/05/2026   | 10/05/2026      | <https://000057.awsstudygroup.com>                                                                                 |

### Kết quả đạt được Tuần 1:

- Hiểu được điện toán đám mây là gì và nắm được các nhóm dịch vụ AWS cơ bản:
  - Compute
  - Storage
  - Networking
  - Database

- Tạo và bảo mật thành công tài khoản AWS Free Tier:
  - Bật MFA cho root account
  - Thiết lập AWS Budgets với cảnh báo qua email

- Nắm được AWS IAM và cách kiểm soát quyền truy cập:
  - Phân biệt User, Group, Role, Policy
  - Tạo IAM User riêng thay vì dùng root account
  - Áp dụng nguyên tắc least privilege
  - Đọc hiểu cấu trúc Policy (Effect, Action, Resource)

- Hiểu và dựng được hạ tầng mạng cơ bản với Amazon VPC:
  - Phân chia public subnet và private subnet
  - Cấu hình Route Table và Internet Gateway
  - Phân biệt Security Group (stateful) và Network ACL (stateless)

- Khởi tạo và kết nối được máy chủ ảo Amazon EC2:
  - Chọn AMI và instance type phù hợp
  - Kết nối qua SSH bằng key pair
  - Gán IAM Role cho EC2 thay vì lưu Access Key trên máy chủ

- Cài đặt và cấu hình AWS CLI trên máy tính, bao gồm:
  - Access Key
  - Secret Key
  - Default Region

- Sử dụng AWS CLI để thực hiện các thao tác cơ bản như:
  - Kiểm tra thông tin tài khoản đang sử dụng
  - Lấy danh sách các region
  - Tạo bucket và upload file lên S3
  - Bật static website hosting

- Host thành công một trang web tĩnh trên Amazon S3 và hiểu cách bucket policy ảnh hưởng đến quyền truy cập công khai.
- Có khả năng thao tác song song giữa giao diện web (Console) và dòng lệnh (CLI) để quản lý tài nguyên AWS.
