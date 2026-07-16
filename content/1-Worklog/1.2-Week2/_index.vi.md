---
title: "Worklog Tuần 2"
date: 2026-05-11
weight: 2
chapter: false
pre: " <b> 2.1. </b> "
---

### Mục tiêu Tuần 2:

- Nắm được cơ sở dữ liệu quan hệ trên AWS với Amazon RDS.
- Hiểu các giải pháp đơn giản hóa (Lightsail) và khả năng co giãn (Auto Scaling).
- Biết cách giám sát hệ thống với CloudWatch và quản lý DNS với Route 53.

### Các công việc thực hiện trong tuần:

| Ngày | Công việc                                                                                                                                                                                                                                                                                   | Ngày bắt đầu | Ngày hoàn thành | Tài liệu tham khảo                                                         |
| ---- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------ | --------------- | -------------------------------------------------------------------------- |
| 2    | - Tìm hiểu Amazon RDS: <br>&emsp; + Các database engine được hỗ trợ <br>&emsp; + Multi-AZ <br>&emsp; + Read Replica <br> - **Thực hành:** <br>&emsp; + Khởi tạo RDS instance trong private subnet <br>&emsp; + Kết nối tới RDS từ EC2 cùng VPC <br>&emsp; + Cấu hình Security Group cho RDS | 11/05/2026   | 11/05/2026      | <https://000005.awsstudygroup.com>                                         |
| 3    | - Tìm hiểu Amazon Lightsail và trường hợp sử dụng <br> - Tìm hiểu Lightsail Containers <br> - So sánh Lightsail với EC2 <br> - **Thực hành:** <br>&emsp; + Tạo Lightsail instance với ứng dụng mẫu                                                                                          | 12/05/2026   | 12/05/2026      | <https://000045.awsstudygroup.com> <br> <https://000046.awsstudygroup.com> |
| 4    | - Tìm hiểu EC2 Auto Scaling: <br>&emsp; + Auto Scaling Group <br>&emsp; + Launch Template <br>&emsp; + Scaling policy (target tracking, step, scheduled) <br> - **Thực hành:** <br>&emsp; + Cấu hình ASG với min/max/desired capacity                                                       | 13/05/2026   | 13/05/2026      | <https://000006.awsstudygroup.com>                                         |
| 5    | - Tìm hiểu Amazon CloudWatch: <br>&emsp; + Metrics, Alarms <br>&emsp; + Logs, Dashboards <br> - **Thực hành:** <br>&emsp; + Tạo alarm cảnh báo khi CPU vượt ngưỡng <br>&emsp; + Kết nối alarm với Auto Scaling                                                                              | 14/05/2026   | 14/05/2026      | <https://000008.awsstudygroup.com>                                         |
| 6    | - Tìm hiểu Amazon Route 53: <br>&emsp; + Các loại record (A, CNAME, Alias) <br>&emsp; + Routing policy (simple, weighted, latency, failover) <br>&emsp; + Health check <br> - **Thực hành:** <br>&emsp; + Tạo hosted zone và cấu hình record                                                | 15/05/2026   | 15/05/2026      | <https://000010.awsstudygroup.com>                                         |
| 7    | - Tìm hiểu AWS Cloud9 (IDE trên cloud) <br> - **Thực hành:** <br>&emsp; + Tạo Cloud9 environment <br>&emsp; + Dùng terminal tích hợp chạy lệnh AWS CLI <br> - Tổng hợp kiến thức tuần 2                                                                                                     | 16/05/2026   | 16/05/2026      | <https://000049.awsstudygroup.com>                                         |

### Kết quả đạt được Tuần 2:

- Nắm được cơ sở dữ liệu được quản lý trên AWS với Amazon RDS:
  - Các database engine được hỗ trợ
  - Vai trò của Multi-AZ trong đảm bảo độ sẵn sàng
  - Vai trò của Read Replica trong mở rộng khả năng đọc
  - Khởi tạo RDS trong private subnet và kết nối từ EC2

- Hiểu được Amazon Lightsail như một lựa chọn đơn giản hóa:
  - Trường hợp phù hợp dùng Lightsail thay vì EC2
  - Lightsail Containers để chạy container không cần quản lý hạ tầng

- Nắm được cơ chế co giãn tự động với EC2 Auto Scaling:
  - Auto Scaling Group và Launch Template
  - Phân biệt các loại scaling policy
  - Cấu hình min/max/desired capacity

- Biết cách giám sát hệ thống với Amazon CloudWatch:
  - Tạo và đọc Metrics
  - Cấu hình Alarms theo ngưỡng
  - Thu thập Logs
  - Xây dựng Dashboards
  - Kết nối alarm với Auto Scaling để kích hoạt co giãn

- Nắm được cách quản lý DNS với Amazon Route 53:
  - Phân biệt các loại record
  - Hiểu các routing policy và trường hợp áp dụng
  - Vai trò của health check

- Làm quen với môi trường phát triển AWS Cloud9 và lợi ích khi code trên môi trường có sẵn AWS CLI.
- Hiểu mối liên hệ giữa các dịch vụ khi kết hợp: RDS trong private subnet, EC2 truy cập qua Security Group, Auto Scaling phối hợp CloudWatch.
