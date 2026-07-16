---
title: "Worklog Tuần 8"
date: 2026-06-22
weight: 8
chapter: false
pre: " <b> 1.8. </b> "
---

### Mục tiêu Tuần 8:

- Xây dựng module Restaurant: mỗi chủ nhà hàng quản lý một nhà hàng.
- Tự động sinh danh sách bàn kèm QR code, có cơ chế thu hồi (revoke) QR.
- Xây dựng module Floor Tables (sơ đồ bàn theo tầng/khu vực).

### Các công việc thực hiện trong tuần:

| Ngày | Công việc                                                                                                                                                                                                                                                                 | Ngày bắt đầu | Ngày hoàn thành | Tài liệu tham khảo                           |
| ---- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------ | --------------- | -------------------------------------------- |
| 2    | - Thiết kế model Restaurant: <br>&emsp; + name, address, phone, status <br>&emsp; + Ràng buộc mỗi owner một nhà hàng <br> - **Thực hành:** <br>&emsp; + Viết `POST /restaurants` nhận thêm `tableCount` <br>&emsp; + Test API bằng curl                                   | 22/06/2026   | 22/06/2026      | <https://github.com/MT-KS-04/smart-menu-api> |
| 3    | - Xây dựng cơ chế sinh bàn và QR secret: <br>&emsp; + Sinh `tableCount` bàn tự động <br>&emsp; + Mỗi bàn gắn `qrSecret` random bằng crypto <br> - **Thực hành:** <br>&emsp; + Điều chỉnh schema: nhúng mảng tables vào Restaurant <br>&emsp; + Viết `GET /restaurants/me` | 23/06/2026   | 23/06/2026      | <https://github.com/MT-KS-04/smart-menu-api> |
| 4    | - Xây dựng API lấy QR của từng bàn: <br>&emsp; + Backend trả payload, FE render ảnh QR <br>&emsp; + Kiểm tra quyền sở hữu nhà hàng <br> - **Thực hành:** <br>&emsp; + Viết `GET /restaurants/:id/tables/:tableNumber/qr`                                                  | 24/06/2026   | 24/06/2026      | <https://github.com/MT-KS-04/smart-menu-api> |
| 5    | - Xây dựng chức năng revoke/regenerate QR: <br>&emsp; + Sinh `qrSecret` mới, QR cũ hết hiệu lực <br>&emsp; + Mục đích: xử lý khi QR bị sao chép <br> - **Thực hành:** <br>&emsp; + Viết `POST /.../qr/revoke` <br>&emsp; + Test luồng tạo → lấy QR → revoke               | 25/06/2026   | 25/06/2026      | <https://github.com/MT-KS-04/smart-menu-api> |
| 6    | - Thiết kế model FloorTable: <br>&emsp; + floor, zone, seats <br>&emsp; + tableNumber, status <br>&emsp; + Tách riêng với bàn gắn QR <br> - **Thực hành:** <br>&emsp; + Viết `POST /floor-tables` và `GET /floor-tables`                                                  | 26/06/2026   | 26/06/2026      | <https://github.com/MT-KS-04/smart-menu-api> |
| 7    | - Hoàn thiện Floor Tables: <br>&emsp; + `PATCH /floor-tables/:id` <br>&emsp; + `DELETE /floor-tables/:id` <br>&emsp; + Route public cho khách xem sơ đồ <br> - Phối hợp với frontend ghép màn hình quản lý bàn của app owner                                              | 27/06/2026   | 27/06/2026      | <https://github.com/MT-KS-04/smart-menu-fe>  |

### Kết quả đạt được Tuần 8:

- Hoàn thành module Restaurant:
  - Chủ nhà hàng tạo được nhà hàng với thông tin cơ bản
  - Ràng buộc mỗi owner chỉ sở hữu một nhà hàng
  - API `GET /restaurants/me` lấy thông tin nhà hàng của mình

- Xây dựng được cơ chế sinh bàn và QR code tự động:
  - Tự sinh số bàn theo `tableCount` khi tạo nhà hàng
  - Mỗi bàn có `qrSecret` random riêng biệt
  - Backend trả payload, frontend render ảnh QR phía client để giảm tải server

- Hoàn thành cơ chế bảo mật cho QR code:
  - API lấy QR có kiểm tra quyền sở hữu nhà hàng
  - Chức năng revoke/regenerate khi QR bị sao chép hoặc lộ
  - QR cũ tự hết hiệu lực sau khi revoke

- Hoàn thành module Floor Tables (sơ đồ mặt bằng):
  - CRUD đầy đủ: tạo, xem, sửa, xóa
  - Quản lý theo tầng, khu vực, số ghế, trạng thái
  - Route public cho khách xem sơ đồ chọn bàn không cần đăng nhập

- Nắm được kinh nghiệm thiết kế dữ liệu với MongoDB:
  - Cân nhắc giữa nhúng (embed) và tách collection tùy theo khối lượng và cách truy vấn
  - Đặt tên rõ ràng cho các khái niệm gần giống nhau (`tables` vs `floor-tables`)

- Phối hợp được với frontend để ghép màn hình quản lý bàn của app owner.
