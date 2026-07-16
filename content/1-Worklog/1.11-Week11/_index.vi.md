---
title: "Worklog Tuần 11"
date: 2026-07-13
weight: 11
chapter: false
pre: " <b> 1.11. </b> "
---

### Mục tiêu Tuần 11:

- Xây dựng chức năng thanh toán tiền mặt và quản lý lịch sử thanh toán, hoàn tiền.
- Xây dựng chức năng đặt bàn (owner tạo và khách tự đặt).
- Xây dựng chức năng cấu hình giờ hoạt động theo từng ngày trong tuần.
- Song song: hoàn thiện cấu hình CloudFront cho các app frontend trên AWS.

### Các công việc thực hiện trong tuần:

| Ngày | Công việc                                                                                                                                                                                                                                                                                                    | Ngày bắt đầu | Ngày hoàn thành | Tài liệu tham khảo                           |
| ---- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------ | --------------- | -------------------------------------------- |
| 2    | - Thiết kế model Payment: <br>&emsp; + sessionId, restaurantId <br>&emsp; + Tổng tiền, status (completed / refunded) <br> - **Thực hành:** <br>&emsp; + Viết `POST /orders/session/:id/cash-payment` <br>&emsp; + Gom đơn đang mở, tính tổng, chặn thanh toán lại                                            | 13/07/2026   | 13/07/2026      | <https://github.com/MT-KS-04/smart-menu-api> |
| 3    | - Xây dựng danh sách và phân trang thanh toán: <br>&emsp; + Filter theo status <br>&emsp; + Phân trang (page, limit) <br> - **Thực hành:** <br>&emsp; + Viết `GET /payments` <br>&emsp; + Chuẩn hóa response phân trang cho frontend                                                                         | 14/07/2026   | 14/07/2026      | <https://github.com/MT-KS-04/smart-menu-api> |
| 4    | - Xây dựng chức năng hoàn tiền (refund): <br>&emsp; + Chỉ refund payment đang completed <br>&emsp; + Chặn refund hai lần <br> - **Thực hành:** <br>&emsp; + Viết `POST /payments/:id/refund` <br> - **AWS:** <br>&emsp; + Cấu hình CloudFront behavior `/api/*` trỏ về Lambda Function URL                   | 15/07/2026   | 15/07/2026      | <https://000094.awsstudygroup.com>           |
| 5    | - Thiết kế model Reservation và chức năng đặt bàn phía owner: <br>&emsp; + customerName, customerPhone, time, partySize <br>&emsp; + Pipeline: pending → confirmed → seated → completed <br> - **Thực hành:** <br>&emsp; + Viết `POST /reservations`, `GET /reservations`, `PATCH /reservations/:id/status`  | 16/07/2026   | 16/07/2026      | <https://github.com/MT-KS-04/smart-menu-api> |
| 6    | - Xây dựng đặt bàn cho khách và giờ hoạt động: <br>&emsp; + Route public khách tự đặt (status pending chờ duyệt) <br>&emsp; + Model OperatingHours: isOpen, openTime, closeTime <br> - **Thực hành:** <br>&emsp; + Viết `GET/PATCH /operating-hours` <br>&emsp; + Validate `openTime` phải trước `closeTime` | 17/07/2026   | 17/07/2026      | <https://github.com/MT-KS-04/smart-menu-api> |
| 7    | - Hoàn thiện các route public còn lại <br> - Phối hợp frontend ghép màn hình payments, reservations và form đặt bàn <br> - **AWS:** <br>&emsp; + Cấu hình CloudFront Function xử lý SPA routing cho 3 app <br>&emsp; + Đồng bộ lại build lên S3 và tạo invalidation                                          | 18/07/2026   | 18/07/2026      | <https://github.com/MT-KS-04/smart-menu-fe>  |

### Kết quả đạt được Tuần 11:

- Hoàn thành chức năng thanh toán tiền mặt:
  - Gom toàn bộ đơn đang mở của một session để tính tổng
  - Chỉ tính đơn chưa hủy
  - Đánh dấu các đơn thành completed và ghi nhận một Payment
  - Chặn thanh toán lại cho session đã thanh toán

- Hoàn thành quản lý lịch sử thanh toán:
  - Liệt kê payment với filter theo trạng thái
  - Phân trang chuẩn (total, page, limit, data)
  - Chức năng hoàn tiền (refund) cho payment đang completed
  - Chặn refund hai lần với thông báo lỗi rõ ràng

- Hoàn thành chức năng đặt bàn (Reservations):
  - Owner tạo, xem danh sách và duyệt đặt bàn
  - Khách tự đặt qua route public, mặc định trạng thái pending chờ duyệt
  - Pipeline trạng thái: pending → confirmed → seated → completed, hoặc cancelled / no_show
  - Filter theo trạng thái và phân trang

- Hoàn thành chức năng cấu hình giờ hoạt động:
  - Cấu hình theo từng ngày trong tuần (Thứ 2 - Chủ nhật)
  - Mỗi ngày có trạng thái mở/đóng và giờ mở/đóng cửa
  - Validate giờ hợp lệ (`openTime` phải trước `closeTime`)
  - Route public để landing/tablet hiển thị giờ mở cửa

- Hoàn thiện cấu hình triển khai trên AWS:
  - Cấu hình CloudFront behavior `/api/*` trỏ về Lambda Function URL
  - Cấu hình CloudFront Function xử lý SPA routing cho 3 app (owner, tablet, landing)
  - Đồng bộ build lên S3 và tạo invalidation sau mỗi lần cập nhật
