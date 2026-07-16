---
title: "Worklog Tuần 3"
date: 2026-05-18
weight: 3
chapter: false
pre: " <b> 3.1. </b> "
---

### Mục tiêu Tuần 3:

- Nắm được cơ sở dữ liệu NoSQL với Amazon DynamoDB và caching với ElastiCache.
- Hiểu cách phân phối nội dung với CloudFront và điện toán biên với Lambda@Edge.
- Củng cố kiến thức mạng nâng cao và xây dựng ứng dụng web có độ sẵn sàng cao.

### Các công việc thực hiện trong tuần:

| Ngày | Công việc                                                                                                                                                                                                                                                                         | Ngày bắt đầu | Ngày hoàn thành | Tài liệu tham khảo                 |
| ---- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------ | --------------- | ---------------------------------- |
| 2    | - Tìm hiểu Amazon DynamoDB: <br>&emsp; + Table, Item, Attribute <br>&emsp; + Partition key, Sort key <br>&emsp; + Capacity mode (On-Demand / Provisioned) <br>&emsp; + GSI, LSI <br> - **Thực hành:** <br>&emsp; + Tạo bảng bằng AWS CLI <br>&emsp; + Thao tác put-item, get-item | 18/05/2026   | 18/05/2026      | <https://000060.awsstudygroup.com> |
| 3    | - Tìm hiểu Amazon ElastiCache: <br>&emsp; + Engine Redis và Memcached <br>&emsp; + Mô hình cache-aside <br>&emsp; + Vai trò của cache trong giảm tải database <br> - **Thực hành:** <br>&emsp; + Tạo ElastiCache cluster                                                          | 19/05/2026   | 19/05/2026      | <https://000061.awsstudygroup.com> |
| 4    | - Tìm hiểu Amazon CloudFront: <br>&emsp; + Edge Location <br>&emsp; + Distribution, Origin <br>&emsp; + Cache behavior, TTL <br> - **Thực hành:** <br>&emsp; + Tạo distribution với origin là S3 <br>&emsp; + Tạo invalidation để cập nhật cache                                  | 20/05/2026   | 20/05/2026      | <https://000094.awsstudygroup.com> |
| 5    | - Tìm hiểu Lambda@Edge: <br>&emsp; + Khái niệm điện toán biên <br>&emsp; + 4 loại trigger (viewer/origin request & response) <br> - **Thực hành:** <br>&emsp; + Xem ví dụ function tùy biến response                                                                              | 21/05/2026   | 21/05/2026      | <https://000130.awsstudygroup.com> |
| 6    | - Networking on AWS Workshop: <br>&emsp; + Ôn lại VPC, subnet, routing <br>&emsp; + Các kịch bản mạng nâng cao <br> - **Thực hành:** <br>&emsp; + Cấu hình mạng theo hướng dẫn workshop                                                                                           | 22/05/2026   | 22/05/2026      | <https://000092.awsstudygroup.com> |
| 7    | - Building Highly Available Web Applications: <br>&emsp; + Kết hợp nhiều AZ <br>&emsp; + Auto Scaling và cân bằng tải <br> - **Thực hành:** <br>&emsp; + Dựng kiến trúc web có độ sẵn sàng cao <br> - Tổng hợp kiến thức phần Explore                                             | 23/05/2026   | 23/05/2026      | <https://000101.awsstudygroup.com> |

### Kết quả đạt được Tuần 3:

- Nắm được cơ sở dữ liệu NoSQL Amazon DynamoDB:
  - Phân biệt partition key và sort key
  - Hiểu capacity mode On-Demand và Provisioned
  - Vai trò của GSI và LSI khi cần truy vấn theo trường khác
  - Thao tác dữ liệu bằng CLI: create-table, put-item, get-item
  - Hiểu tư duy thiết kế bảng phải xuất phát từ access pattern

- Hiểu vai trò của caching với Amazon ElastiCache:
  - Phân biệt Redis và Memcached
  - Mô hình cache-aside
  - Cách cache giúp giảm tải database và tăng tốc truy vấn

- Nắm được cách phân phối nội dung với Amazon CloudFront:
  - Vai trò của mạng lưới Edge Location
  - Cấu hình distribution, origin, cache behavior
  - Hiểu TTL và cách dùng invalidation để cập nhật nội dung mới

- Hiểu khái niệm điện toán biên với Lambda@Edge:
  - Ý nghĩa của việc chạy code tại Edge Location
  - Phân biệt 4 loại trigger và trường hợp sử dụng

- Củng cố và nâng cao kiến thức mạng trên AWS qua Networking Workshop.

- Xây dựng được ứng dụng web có độ sẵn sàng cao, hiểu cách kết hợp:
  - Nhiều Availability Zone
  - Auto Scaling
  - Cân bằng tải
  - Giám sát

- Hoàn thành phần Explore AWS Services, có cái nhìn tổng thể về các dịch vụ nền tảng.
