---
title: "Worklog Tuần 5"
date: 2026-06-01
weight: 5
chapter: false
pre: " <b> 5.1. </b> "
---

### Mục tiêu Tuần 5:

- Nắm được Infrastructure as Code với AWS CloudFormation và AWS CDK.
- Hiểu cách quản lý giới hạn dịch vụ với Service Quotas.
- Biết cách theo dõi, phân tích chi phí và tối ưu tài nguyên trên AWS.

### Các công việc thực hiện trong tuần:

| Ngày | Công việc                                                                                                                                                                                                                                                                                             | Ngày bắt đầu | Ngày hoàn thành | Tài liệu tham khảo                 |
| ---- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------ | --------------- | ---------------------------------- |
| 2    | - Tìm hiểu Infrastructure as Code (IaC) <br> - Tìm hiểu AWS CloudFormation: <br>&emsp; + Cấu trúc template (Resources, Parameters, Outputs) <br>&emsp; + Stack và Change set <br> - **Thực hành:** <br>&emsp; + Viết và deploy một template tạo tài nguyên <br>&emsp; + Kiểm tra tài nguyên của stack | 01/06/2026   | 01/06/2026      | <https://000037.awsstudygroup.com> |
| 3    | - Tìm hiểu AWS CDK: <br>&emsp; + Construct, Stack, App <br>&emsp; + So sánh CDK với CloudFormation thuần <br> - **Thực hành:** <br>&emsp; + Khởi tạo CDK project <br>&emsp; + Chạy `cdk synth` và `cdk bootstrap` <br>&emsp; + Deploy stack bằng CDK                                                  | 02/06/2026   | 02/06/2026      | <https://000038.awsstudygroup.com> |
| 4    | - Tìm hiểu Service Quotas: <br>&emsp; + Ý nghĩa của giới hạn dịch vụ <br>&emsp; + Cách xem quota hiện tại <br>&emsp; + Quy trình yêu cầu tăng quota <br> - **Thực hành:** <br>&emsp; + Kiểm tra quota của một số dịch vụ                                                                              | 03/06/2026   | 03/06/2026      | <https://000063.awsstudygroup.com> |
| 5    | - Tìm hiểu Cost and Usage Management: <br>&emsp; + Cost Explorer <br>&emsp; + Cost and Usage Report (CUR) <br>&emsp; + Phân bổ chi phí theo tag <br> - **Thực hành:** <br>&emsp; + Phân tích xu hướng chi phí trên Cost Explorer                                                                      | 04/06/2026   | 04/06/2026      | <https://000064.awsstudygroup.com> |
| 6    | - Tìm hiểu EC2 Resource Optimization: <br>&emsp; + Khái niệm right-sizing <br>&emsp; + Dựa vào metric để chọn instance type <br>&emsp; + Công cụ đưa ra khuyến nghị tối ưu <br> - **Thực hành:** <br>&emsp; + Đánh giá kích thước một instance                                                        | 05/06/2026   | 05/06/2026      | <https://000032.awsstudygroup.com> |
| 7    | - Tìm hiểu VPC Flow Logs: <br>&emsp; + Cấu trúc một bản ghi flow log <br>&emsp; + Đẩy log sang CloudWatch Logs hoặc S3 <br> - **Thực hành:** <br>&emsp; + Bật flow log và phân tích bản ghi <br>&emsp; + Lọc theo ACCEPT/REJECT <br> - Tổng hợp kiến thức tuần 5                                      | 06/06/2026   | 06/06/2026      | <https://000074.awsstudygroup.com> |

### Kết quả đạt được Tuần 5:

- Hiểu và áp dụng được Infrastructure as Code với AWS CloudFormation:
  - Cấu trúc một template: Resources, Parameters, Outputs
  - Khái niệm stack và change set
  - Deploy hạ tầng từ template thay vì bấm tay trên Console
  - Nắm được YAML nhạy cảm với thụt lề, cần cẩn thận khi viết

- Nắm được AWS CDK và cách viết hạ tầng bằng ngôn ngữ lập trình:
  - Khái niệm construct, stack, app
  - Vòng đời: init → synth → bootstrap → deploy
  - Hiểu account mới phải chạy `cdk bootstrap` một lần trước khi deploy
  - So sánh được ưu điểm của CDK so với viết YAML thuần

- Hiểu vai trò của Service Quotas trong vận hành:
  - Ảnh hưởng của quota tới khả năng mở rộng hệ thống
  - Cách kiểm tra và yêu cầu tăng quota khi cần

- Biết cách theo dõi và quản lý chi phí trên AWS:
  - Phân tích xu hướng chi phí bằng Cost Explorer
  - Hiểu Cost and Usage Report
  - Dùng tag để phân bổ chi phí theo nhóm

- Nắm được cách tối ưu tài nguyên với right-sizing:
  - Dựa vào metric thay vì cảm tính để chọn instance type
  - Cân bằng giữa chi phí và hiệu năng

- Giám sát mạng với VPC Flow Logs:
  - Đọc và hiểu cấu trúc bản ghi flow log
  - Lọc theo ACCEPT/REJECT để chẩn đoán kết nối và kiểm tra bảo mật
