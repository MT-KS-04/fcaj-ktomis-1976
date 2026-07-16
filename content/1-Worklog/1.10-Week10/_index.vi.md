---
title: "Worklog Tuần 10"
date: 2026-07-06
weight: 10
chapter: false
pre: " <b> 1.10. </b> "
---

### Mục tiêu Tuần 10:

- Xây dựng chức năng phiên khách (guest session) qua quét QR, không cần tài khoản.
- Xây dựng menu công khai kèm cảnh báo dị ứng theo mức độ (đỏ/vàng/xanh).
- Xây dựng chức năng đặt món và quản lý đơn theo luồng trạng thái.
- Song song: đồng bộ frontend lên S3 và kiểm tra qua CloudFront.

### Các công việc thực hiện trong tuần:

| Ngày | Công việc                                                                                                                                                                                                                                                                                                       | Ngày bắt đầu | Ngày hoàn thành | Tài liệu tham khảo                           |
| ---- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------ | --------------- | -------------------------------------------- |
| 2    | - Thiết kế model Session: <br>&emsp; + restaurantId, tableNumber <br>&emsp; + allergens, preferences <br>&emsp; + status, expiresAt <br> - **Thực hành:** <br>&emsp; + Viết `POST /sessions` verify `qrSecret` trước khi tạo session                                                                            | 06/07/2026   | 06/07/2026      | <https://github.com/MT-KS-04/smart-menu-api> |
| 3    | - Xây dựng cơ chế hết hạn session và khai báo dị ứng: <br>&emsp; + Session tự hết hạn khi không hoạt động <br>&emsp; + Khách khai dị ứng và khẩu vị <br> - **Thực hành:** <br>&emsp; + Viết `PATCH /sessions/:id/allergens`                                                                                     | 07/07/2026   | 07/07/2026      | <https://github.com/MT-KS-04/smart-menu-api> |
| 4    | - Xây dựng menu công khai kèm cảnh báo dị ứng: <br>&emsp; + Đối chiếu allergen của món với khai báo của khách <br>&emsp; + Nhãn đỏ (chứa) / vàng (có thể chứa) / xanh (an toàn) <br> - **Thực hành:** <br>&emsp; + Viết `GET /public/restaurants/:id/menu`                                                      | 08/07/2026   | 08/07/2026      | <https://github.com/MT-KS-04/smart-menu-api> |
| 5    | - Thiết kế model Order và chức năng đặt món: <br>&emsp; + sessionId, items, customerNotes, status <br>&emsp; + Kiểm tra món thuộc menu published và available <br> - **Thực hành:** <br>&emsp; + Viết `POST /orders` cho khách <br> - **AWS:** <br>&emsp; + Đồng bộ bản build frontend lên S3 (`aws s3 sync`)   | 09/07/2026   | 09/07/2026      | <https://000057.awsstudygroup.com>           |
| 6    | - Xây dựng luồng trạng thái đơn hàng: <br>&emsp; + `pending` → `confirmed` → `preparing` → `ready` → `served` → `completed` <br>&emsp; + Chặn nhảy lùi hoặc nhảy cóc trạng thái <br> - **Thực hành:** <br>&emsp; + Viết `PATCH /orders/:id/status` <br>&emsp; + Viết `GET /orders` và `GET /orders/session/:id` | 10/07/2026   | 10/07/2026      | <https://github.com/MT-KS-04/smart-menu-api> |
| 7    | - Phối hợp frontend ghép app tablet và owner <br> - **AWS:** <br>&emsp; + Tạo CloudFront distribution với origin là S3 <br>&emsp; + Tạo invalidation cập nhật nội dung mới <br>&emsp; + Kiểm tra luồng end-to-end trên môi trường AWS                                                                           | 11/07/2026   | 11/07/2026      | <https://000094.awsstudygroup.com>           |

### Kết quả đạt được Tuần 10:

- Hoàn thành chức năng phiên khách (guest session):
  - Khách quét QR trên bàn để mở session, không cần đăng ký tài khoản
  - Verify `qrSecret` trước khi tạo session, QR đã revoke không dùng được
  - Session tự hết hạn sau khoảng thời gian không hoạt động
  - Khách khai báo dị ứng và khẩu vị gắn theo session

- Hoàn thành menu công khai với cảnh báo dị ứng:
  - Trả về menu đang published kèm danh sách món
  - Đối chiếu allergen của món với khai báo của khách
  - Gắn nhãn cảnh báo theo 3 mức:
    - Đỏ: món chứa chất khách dị ứng
    - Vàng: món có thể chứa
    - Xanh: món an toàn

- Hoàn thành chức năng đặt món cho khách:
  - Đặt món theo session, không cần đăng nhập
  - Ghi chú theo món và ghi chú chung cho đơn
  - Kiểm tra món phải thuộc menu published và đang available

- Hoàn thành quản lý đơn hàng theo luồng trạng thái:
  - Pipeline một chiều: pending → confirmed → preparing → ready → served → completed
  - Chặn chuyển trạng thái nhảy lùi hoặc nhảy cóc
  - Owner xem và xử lý đơn của nhà hàng
  - Khách theo dõi trạng thái đơn của mình

- Triển khai và kiểm tra dự án trên AWS:
  - Đồng bộ bản build frontend lên S3
  - Tạo CloudFront distribution với origin là S3
  - Tạo invalidation để cập nhật nội dung mới sau mỗi lần build
  - Kiểm tra luồng end-to-end trên môi trường AWS

- Chạy được kịch bản hoàn chỉnh: quét QR → xem menu → đặt món → owner xử lý → khách thấy cập nhật.
