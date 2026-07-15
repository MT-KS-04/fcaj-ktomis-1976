---
title: "Worklog Tuần 3"
date: 2026-05-18
weight: 3
chapter: false
pre: " <b> 3.1. </b> "
---

## Thông tin chung

| Nội dung         | Chi tiết                                                                          |
| ---------------- | --------------------------------------------------------------------------------- |
| Thời gian        | 18/05/2026 - 24/05/2026                                                           |
| Tuần thực tập    | Tuần 3                                                                            |
| Giai đoạn        | Explore AWS Services (nâng cao)                                                   |
| Chương trình học | First Cloud Journey                                                               |
| Chủ đề chính     | NoSQL, caching, CDN, edge computing, mạng nâng cao và ứng dụng có độ sẵn sàng cao |
| Mục tiêu tuần    | Nắm DynamoDB, ElastiCache, CloudFront, Lambda@Edge, networking nâng cao và HA web |

## Định hướng học tập Tuần 3

Tuần 3 khép lại phần **Explore AWS Services** với các workshop nặng hơn: cơ sở dữ liệu NoSQL (DynamoDB), caching (ElastiCache), phân phối nội dung (CloudFront), điện toán biên (Lambda@Edge), mạng nâng cao và bài tổng hợp về ứng dụng web độ sẵn sàng cao. Mấy chủ đề này khó hơn hẳn hai tuần trước nên em dành thời gian đọc kỹ hơn và để hai bài nặng nhất vào cuối tuần.

## Mục tiêu học tập Tuần 3

- Tìm hiểu NoSQL Database Essentials with Amazon DynamoDB.
- Tìm hiểu In-Memory Caching with Amazon ElastiCache.
- Tìm hiểu Content Delivery with Amazon CloudFront.
- Tìm hiểu Edge Computing with CloudFront and Lambda@Edge.
- Tìm hiểu Networking on AWS Workshop.
- Tìm hiểu Building Highly Available Web Applications.

## Nội dung thực hiện trong tuần

### Ngày 1 - Thứ hai, 18/05/2026

Chủ đề: **NoSQL Database Essentials with Amazon DynamoDB**.

Nội dung đã thực hiện:

- Đọc về DynamoDB: bảng, item, partition key, sort key.
- Tìm hiểu capacity mode (On-Demand và Provisioned) và index GSI/LSI.
- Làm theo workshop tạo bảng và thử vài thao tác thêm/đọc/xóa item.

Em tạo bảng bằng CLI với partition key là `UserId`:

```bash
aws dynamodb create-table \
  --table-name Users \
  --attribute-definitions AttributeName=UserId,AttributeType=S \
  --key-schema AttributeName=UserId,KeyType=HASH \
  --billing-mode PAY_PER_REQUEST
```

Thêm và đọc thử một item:

```bash
aws dynamodb put-item --table-name Users \
  --item '{"UserId": {"S": "u001"}, "Name": {"S": "Nam"}}'

aws dynamodb get-item --table-name Users \
  --key '{"UserId": {"S": "u001"}}'
```

```json
{
  "Item": {
    "Name": { "S": "Nam" },
    "UserId": { "S": "u001" }
  }
}
```

Có lần em thử `get-item` mà truyền key là `Name` thay vì `UserId` thì bị lỗi:

```
An error occurred (ValidationException): The provided key element does not match the schema
```

Đến đây em mới thấm là DynamoDB chỉ cho query theo key đã định nghĩa, muốn tìm theo trường khác thì phải nghĩ tới GSI ngay từ lúc thiết kế bảng.

Kết quả đạt được:

- Hiểu DynamoDB tư duy khác hẳn database quan hệ, phải nghĩ theo access pattern.
- Tạo và thao tác được dữ liệu trên bảng ở mức cơ bản.
- Nhớ được cấu trúc lệnh `put-item` / `get-item` và bài học phải chọn key cho đúng ngay từ đầu.

### Ngày 2 - Thứ ba, 19/05/2026

Chủ đề: **In-Memory Caching with Amazon ElastiCache**.

Nội dung đã thực hiện:

- Đọc về ElastiCache và hai engine Redis, Memcached.
- Tìm hiểu vì sao caching giúp giảm tải database và tăng tốc truy vấn (mô hình cache-aside).
- Xem hướng dẫn tạo một cluster để hình dung cách nó hoạt động.

Kết quả đạt được:

- Hiểu vai trò của cache và khi nào nên dùng ElastiCache.
- Phân biệt được Redis và Memcached ở mức tổng quan.

### Ngày 3 - Thứ tư, 20/05/2026

Chủ đề: **Content Delivery with Amazon CloudFront**.

Nội dung đã thực hiện:

- Đọc về CloudFront và mạng lưới Edge Location.
- Tìm hiểu distribution, origin, cache behavior, TTL.
- Làm theo workshop tạo thử một distribution lấy origin là bucket S3 đã dựng ở tuần 1.

Sau khi sửa file trên S3 mà trang qua CloudFront vẫn hiện bản cũ, em tạo invalidation để xóa cache:

```bash
aws cloudfront create-invalidation \
  --distribution-id E123ABC456DEF --paths "/*"
```

```json
{
  "Invalidation": {
    "Status": "InProgress",
    "InvalidationBatch": {
      "Paths": { "Quantity": 1, "Items": ["/*"] }
    }
  }
}
```

Chờ status chuyển sang `Completed` thì nội dung mới mới hiện. Đây là lúc em hiểu ra vì sao "sửa file xong mà web không đổi" — do TTL vẫn còn hiệu lực ở Edge.

Kết quả đạt được:

- Hiểu CloudFront giúp phân phối nội dung gần người dùng để giảm độ trễ.
- Tạo được distribution đơn giản theo hướng dẫn.
- Nhớ lệnh `create-invalidation` để lần sau sửa nội dung xong biết cách ép cache cập nhật.

### Ngày 4 - Thứ năm, 21/05/2026

Chủ đề: **Edge Computing with CloudFront and Lambda@Edge**.

Nội dung đã thực hiện:

- Đọc về Lambda@Edge và ý tưởng chạy code ngay tại Edge Location.
- Tìm hiểu 4 loại trigger: viewer request/response, origin request/response.
- Xem ví dụ một function nhỏ tùy biến response để hiểu cách áp dụng.

Kết quả đạt được:

- Nắm khái niệm điện toán biên và vai trò của Lambda@Edge.
- Hiểu sơ bộ 4 loại trigger dùng vào việc gì.

### Ngày 5 - Thứ sáu, 22/05/2026

Chủ đề: **Networking on AWS Workshop**.

Nội dung đã thực hiện:

- Đọc lại và mở rộng phần mạng: VPC, subnet, routing ở các tình huống phức tạp hơn tuần 1.
- Làm theo workshop từng bước để củng cố phần mạng.

Kết quả đạt được:

- Chắc hơn phần networking, đỡ lơ mơ so với lúc học VPC lần đầu.

### Ngày 6 - Thứ bảy, 23/05/2026

Chủ đề: **Building Highly Available Web Applications**.

Nội dung đã thực hiện:

- Đọc bài tổng hợp về xây dựng web app độ sẵn sàng cao.
- Làm theo hướng dẫn ghép nhiều AZ, Auto Scaling và cân bằng tải lại với nhau.
- Ngồi tổng hợp kiến thức cả tuần và cả phần Explore.

Kết quả đạt được:

- Hình dung được cách các dịch vụ đã học ghép lại thành một hệ thống có tính sẵn sàng.
- Thấy rõ hơn mối liên hệ giữa những thứ học rời rạc trước đó.

## Tổng kết kiến thức Tuần 3

| Nhóm kiến thức    | Nội dung đã học                                       |
| ----------------- | ----------------------------------------------------- |
| NoSQL Database    | DynamoDB, partition/sort key, capacity mode, GSI/LSI  |
| Caching           | ElastiCache, Redis, Memcached, cache-aside            |
| Content Delivery  | CloudFront, distribution, origin, cache behavior, TTL |
| Edge Computing    | Lambda@Edge, các loại trigger                         |
| Networking        | Networking on AWS Workshop                            |
| High Availability | Building Highly Available Web Applications            |

## Kết quả đạt được trong tuần

- Tạo và thao tác thử được dữ liệu trên DynamoDB.
- Hiểu vai trò của ElastiCache và cách tạo cluster.
- Tạo được CloudFront distribution và biết Lambda@Edge dùng để làm gì.
- Củng cố lại phần mạng nâng cao.
- Nắm được cách dựng một web app độ sẵn sàng cao theo workshop.

## Khó khăn gặp phải

- DynamoDB làm em khó chịu nhất tuần này, vì quen tư duy bảng quan hệ nên lúc thiết kế partition key cứ sai, phải nghĩ lại từ đầu theo cách truy vấn.
- CloudFront cache xong em sửa file mà mãi không thấy cập nhật, hóa ra là do TTL và phải làm invalidation mới hiểu.
- Bài web app độ sẵn sàng cao nhiều thành phần quá, đọc một lần không nhớ nổi, em phải vẽ sơ đồ ra mới theo được.

## Bài học rút ra

- Em nhận ra DynamoDB không phải cứ đổi tên từ SQL sang là dùng được, phải nghĩ theo cách mình sẽ truy vấn dữ liệu.
- Cache giúp nhanh thật nhưng cũng dễ gây rối nếu không hiểu TTL, nên phải cẩn thận chứ không bật đại.
- Mấy bài tổng hợp cuối phần Explore giúp em nối lại những thứ học lẻ tẻ, thấy được bức tranh chung thay vì từng mảnh.

## Kế hoạch cho Tuần 4

- Chuyển sang giai đoạn Migrate to AWS: VM Import/Export, DMS + SCT, Elastic Disaster Recovery.
- Bắt đầu phần Optimize - Operations: Systems Manager, Session Manager, Tags & Resource Groups.

## Nhận xét cuối tuần

Tuần 3 là tuần nặng nhất trong ba tuần đầu, nhất là DynamoDB và bài web app độ sẵn sàng cao. Nhưng học xong phần Explore, em thấy mình đã có cái nhìn tương đối đầy đủ về các dịch vụ nền tảng, đủ để tự tin bước sang phần Migrate và Optimize.
