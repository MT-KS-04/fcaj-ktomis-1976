---
title: "Worklog Tuần 2"
date: 2026-05-10
weight: 2
chapter: false
pre: " <b> 2.1. </b> "
---

## Thông tin chung

| Nội dung         | Chi tiết                                                                       |
| ---------------- | ------------------------------------------------------------------------------ |
| Thời gian        | 10/05/2026 - 16/05/2026                                                        |
| Tuần thực tập    | Tuần 2                                                                         |
| Giai đoạn        | Explore AWS Services                                                           |
| Chương trình học | First Cloud Journey                                                            |
| Chủ đề chính     | Cơ sở dữ liệu, Lightsail, Auto Scaling, giám sát, DNS và môi trường phát triển |
| Mục tiêu tuần    | Nắm RDS, Lightsail, EC2 Auto Scaling, CloudWatch, Route 53 và Cloud9           |

## Định hướng học tập Tuần 2

Tiếp nối phần **Explore AWS Services**, tuần 2 em học các dịch vụ mở rộng trên nền tảng đã có: cơ sở dữ liệu quan hệ (RDS), giải pháp đơn giản hóa (Lightsail), khả năng co giãn (EC2 Auto Scaling), giám sát (CloudWatch), DNS (Route 53) và môi trường phát triển trên cloud (Cloud9). Em vẫn học theo hướng cái nào dễ đọc trước, cái nào cần bấm nhiều hơn thì để sau, mỗi ngày tối đa 1–2 dịch vụ.

## Mục tiêu học tập Tuần 2

- Tìm hiểu Amazon RDS (Relational Database Service).
- Tìm hiểu Amazon Lightsail và Lightsail Containers.
- Tìm hiểu Scaling Applications with EC2 Auto Scaling.
- Tìm hiểu Monitoring with Amazon CloudWatch.
- Tìm hiểu Hybrid DNS Management with Amazon Route 53.
- Tìm hiểu Cloud Development with AWS Cloud9.

## Nội dung thực hiện trong tuần

### Ngày 1 - Thứ hai, 11/05/2026

Chủ đề: **Database Essentials with Amazon RDS**.

Nội dung đã thực hiện:

- Đọc tài liệu RDS: các database engine được hỗ trợ, khái niệm Multi-AZ và Read Replica.
- Làm theo workshop tạo thử một RDS instance đặt trong private subnet.
- Thử kết nối tới RDS từ EC2 trong cùng VPC để xem luồng kết nối.

Lấy endpoint của RDS qua CLI rồi từ EC2 kết nối vào (bài dùng PostgreSQL):

```bash
aws rds describe-db-instances \
  --query "DBInstances[].Endpoint.Address" --output text
```

```
intern-db.abcdefg123.ap-southeast-1.rds.amazonaws.com
```

```bash
psql -h intern-db.abcdefg123.ap-southeast-1.rds.amazonaws.com -U postgres -d postgres
```

Lần đầu em connect từ máy cá nhân nên cứ bị treo rồi timeout, sau mới hiểu RDS nằm trong private subnet, phải SSH vào EC2 cùng VPC rồi mới connect được — với lại Security Group của RDS phải mở port 5432 cho SG của EC2.

Kết quả đạt được:

- Hiểu RDS khác gì so với tự cài database trên EC2.
- Nắm ý nghĩa của Multi-AZ (dự phòng) và Read Replica (mở rộng đọc), dù mới ở mức đọc hiểu.
- Nhớ được là muốn vào RDS private thì phải đi qua một máy trong VPC, không connect thẳng từ ngoài.

### Ngày 2 - Thứ ba, 12/05/2026

Chủ đề: **Simplified Computing with Amazon Lightsail** và **Container Deployment with Amazon Lightsail Containers**.

Nội dung đã thực hiện:

- Đọc về Lightsail và trường hợp nó phù hợp hơn EC2 (ứng dụng nhỏ, muốn đơn giản).
- Làm theo hướng dẫn tạo thử một Lightsail instance với ứng dụng mẫu.
- Đọc thêm phần Lightsail Containers để biết cách chạy container mà không phải lo hạ tầng.

Kết quả đạt được:

- Hiểu khi nào nên chọn Lightsail thay vì EC2.
- Biết Lightsail Containers tồn tại và giải quyết bài toán gì.

### Ngày 3 - Thứ tư, 13/05/2026

Chủ đề: **Scaling Applications with EC2 Auto Scaling**.

Nội dung đã thực hiện:

- Đọc về Auto Scaling Group và Launch Template.
- Tìm hiểu các loại scaling policy: target tracking, step scaling, scheduled scaling.
- Làm theo workshop cấu hình thử một ASG với min/max/desired để xem cách nó co giãn.

Kết quả đạt được:

- Hiểu ý tưởng đằng sau Auto Scaling và vì sao nó giúp tiết kiệm chi phí.
- Phân biệt được sơ bộ các loại scaling policy.

### Ngày 4 - Thứ năm, 14/05/2026

Chủ đề: **Monitoring with Amazon CloudWatch**.

Nội dung đã thực hiện:

- Đọc về CloudWatch: Metrics, Alarms, Logs, Dashboards.
- Làm theo hướng dẫn tạo thử một alarm cảnh báo khi CPU cao.
- Tìm hiểu cách alarm này liên kết với Auto Scaling để kích hoạt co giãn.

Kết quả đạt được:

- Biết CloudWatch dùng để theo dõi cái gì và tạo alarm ra sao.
- Hiểu mối liên hệ giữa CloudWatch và Auto Scaling.

### Ngày 5 - Thứ sáu, 15/05/2026

Chủ đề: **Hybrid DNS Management with Amazon Route 53**.

Nội dung đã thực hiện:

- Đọc về Route 53: các loại record (A, CNAME, Alias) và routing policy.
- Tìm hiểu health check và các kiểu định tuyến (simple, weighted, latency, failover).
- Xem hướng dẫn tạo hosted zone và trỏ record tới tài nguyên AWS.

Kết quả đạt được:

- Hiểu Route 53 làm gì trong việc quản lý tên miền.
- Nắm sơ bộ các routing policy và khi nào dùng cái nào.

### Ngày 6 - Thứ bảy, 16/05/2026

Chủ đề: **Cloud Development with AWS Cloud9**.

Nội dung đã thực hiện:

- Đọc về Cloud9 như một IDE chạy trên cloud.
- Tạo thử một Cloud9 environment và mở terminal tích hợp để gõ vài lệnh AWS CLI.
- Ngồi tổng hợp lại kiến thức cả tuần.

Kết quả đạt được:

- Dùng thử được Cloud9, thấy tiện ở chỗ đã có sẵn AWS CLI.
- Hiểu lợi ích của việc code ngay trên môi trường gần với AWS.

## Tổng kết kiến thức Tuần 2

| Nhóm kiến thức | Nội dung đã học                                   |
| -------------- | ------------------------------------------------- |
| Database       | Amazon RDS, Multi-AZ, Read Replica                |
| Simplified     | Amazon Lightsail, Lightsail Containers            |
| Scalability    | EC2 Auto Scaling, Launch Template, scaling policy |
| Monitoring     | CloudWatch Metrics, Alarms, Logs, Dashboards      |
| DNS            | Route 53, record, routing policy, health check    |
| Development    | AWS Cloud9                                        |

## Kết quả đạt được trong tuần

- Tạo và kết nối thử được RDS từ EC2 theo workshop.
- Biết thêm Lightsail như một lựa chọn đơn giản hơn EC2.
- Cấu hình thử EC2 Auto Scaling và CloudWatch alarm.
- Nắm cách Route 53 quản lý DNS.
- Làm quen môi trường Cloud9.

## Khó khăn gặp phải

- Lúc thử kết nối RDS từ EC2 em bị nghẽn khá lâu, sau mới biết là do Security Group và subnet group của RDS chưa cho phép.
- Auto Scaling em cấu hình xong mà mãi không thấy nó co giãn như trong bài, phải xem lại alarm và policy mới hiểu là ngưỡng mình đặt chưa hợp lý.
- Mấy loại routing policy của Route 53 tên na ná nhau nên ban đầu em cứ nhầm, phải ghi ra giấy theo mục đích từng cái mới nhớ.

## Bài học rút ra

- Em rút ra là để database trong private subnet đúng là an toàn hơn, nhưng đổi lại phải cẩn thận cấu hình mạng chứ không "tạo xong là chạy".
- Auto Scaling với CloudWatch gần như đi liền nhau, hiểu cái này thì mới dùng được cái kia.
- Lightsail hợp với mấy thứ nhỏ gọn, còn cần linh hoạt thì vẫn phải quay về EC2 — không có cái nào tốt cho mọi trường hợp.

## Kế hoạch cho Tuần 3

- Tìm hiểu Amazon DynamoDB và Amazon ElastiCache.
- Tìm hiểu Amazon CloudFront và Lambda@Edge.
- Tìm hiểu Networking on AWS Workshop.
- Thực hành Building Highly Available Web Applications.

## Nhận xét cuối tuần

Tuần 2 kiến thức bắt đầu nhiều hơn, nhất là mấy phần cần cấu hình như RDS và Auto Scaling. Em thấy cứ đọc trước rồi bấm thử theo workshop là cách học hợp với mình, vì nhiều chỗ chỉ khi tự làm mới lòi ra là chưa hiểu.
