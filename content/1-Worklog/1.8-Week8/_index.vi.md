---
title: "Worklog Tuần 8"
date: 2026-06-22
weight: 8
chapter: false
pre: " <b> 1.8. </b> "
---

## Thông tin chung

| Nội dung      | Chi tiết                                                          |
| ------------- | ---------------------------------------------------------------- |
| Thời gian     | 22/06/2026 - 28/06/2026                                          |
| Tuần thực tập | Tuần 8                                                           |
| Giai đoạn     | SmartMenu - Nhà hàng, bàn, QR code và sơ đồ tầng                 |
| Vai trò       | Full-stack, phụ trách backend; FE có hỗ trợ từ thành viên nhóm   |
| Chủ đề chính  | Module Restaurant, sinh QR theo bàn, revoke QR, Floor Tables     |

## Định hướng tuần 8

Có auth rồi thì tuần này mình làm phần "khung" của nhà hàng: mỗi chủ nhà hàng tạo được một restaurant, hệ thống tự sinh danh sách bàn kèm QR code cho từng bàn. QR chính là cửa ngõ để khách vào gọi món nên phải làm cho chắc, có cả cơ chế thu hồi khi cần. Song song đó bắt đầu module sơ đồ tầng (floor tables) để owner sắp bàn theo tầng/khu vực.

## Mục tiêu tuần 8

- Model `Restaurant` + `Table`, mỗi owner một nhà hàng.
- Tự sinh bàn + QR secret theo `tableCount` khi tạo nhà hàng.
- API lấy QR của bàn và revoke/regenerate QR.
- Model + CRUD `FloorTable` (tầng, khu vực, số ghế, số bàn).

## Nội dung thực hiện trong tuần

### Ngày 1 - Thứ hai, 22/06/2026

Thiết kế và tạo nhà hàng.

- Thiết kế model `Restaurant`: name, address, phone, status, ownerId. Ràng buộc mỗi owner chỉ một nhà hàng (unique theo ownerId).
- Viết controller tạo nhà hàng, nhận thêm `tableCount` để biết sinh bao nhiêu bàn.
- Chốt lại ý tưởng data: mỗi bàn có `tableNumber` + `qrSecret` random.

```bash
curl -X POST http://localhost:3000/api/v1/restaurants \
  -H "Authorization: Bearer $ACCESS_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{"name":"Pho 24","address":"123 Test Street","tableCount":10,"phone":"0987654321"}'
```

### Ngày 2 - Thứ ba, 23/06/2026

Sinh bàn + QR secret.

- Viết hàm sinh `tableCount` bàn, mỗi bàn gắn một `qrSecret` random bằng `crypto`.
- Ban đầu mình định lưu bàn thành collection riêng, nhưng thấy số bàn không nhiều nên nhúng luôn mảng `tables` vào document Restaurant cho dễ join - chỉnh lại schema theo hướng đó.
- Thêm `GET /restaurants/me` để owner lấy nhà hàng của mình.

### Ngày 3 - Thứ tư, 24/06/2026

API lấy QR của từng bàn.

- Viết `GET /restaurants/:restaurantId/tables/:tableNumber/qr` trả về dữ liệu để FE render QR.
- Chốt với FE: backend trả payload (restaurantId + tableNumber + qrSecret), còn việc vẽ ảnh QR để FE làm bằng thư viện phía client cho nhẹ server.
- Sửa lại một chút: chỉ owner sở hữu nhà hàng đó mới xem được QR, thêm check quyền trong controller.

### Ngày 4 - Thứ năm, 25/06/2026

Revoke / regenerate QR.

- Viết `POST /restaurants/:restaurantId/tables/:tableNumber/qr/revoke`: sinh `qrSecret` mới, QR cũ tự hết hiệu lực.
- Lý do làm cái này: lỡ QR bị chụp lại dán chỗ khác thì owner revoke được.
- Test lại luồng: tạo nhà hàng -> lấy QR -> revoke -> QR cũ không dùng để tạo session được nữa (phần verify sẽ làm ở tuần session).

Có lỗi nhỏ: lúc revoke mình quên lưu lại document sau khi đổi secret (`.save()`), nên gọi lại vẫn ra secret cũ. Thêm `save` là ổn.

### Ngày 5 - Thứ sáu, 26/06/2026

Bắt đầu Floor Tables.

- Thiết kế model `FloorTable`: floor, zone, seats, tableNumber, status, restaurantId. Cái này tách riêng với danh sách bàn-QR vì nó phục vụ sơ đồ mặt bằng, không phải QR.
- Viết `POST /floor-tables` và `GET /floor-tables`.

```bash
curl -X POST http://localhost:3000/api/v1/floor-tables \
  -H "Authorization: Bearer $ACCESS_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{"floor":1,"zone":"Sân vườn","seats":4,"tableNumber":5}'
```

### Ngày 6 - Thứ bảy, 27/06/2026

Hoàn thiện Floor Tables + ghép FE.

- Viết `PATCH /floor-tables/:id` (đổi zone/seats/status) và `DELETE /floor-tables/:id`.
- Thêm route public `GET /public/restaurants/:restaurantId/floor-tables` để khách xem sơ đồ chọn bàn (không cần auth).
- Ngồi với bạn FE ghép màn hình quản lý bàn của app owner vào các API này, sửa vài chỗ tên field cho khớp với type bên FE.

## Kết quả đạt được trong tuần

- Owner tạo được nhà hàng, hệ thống tự sinh bàn + QR.
- API lấy và revoke QR chạy được, có kiểm tra quyền sở hữu.
- Module Floor Tables CRUD đầy đủ, có route public cho khách xem sơ đồ.
- FE app owner ghép được phần quản lý bàn.

## Khó khăn gặp phải

- Phân vân giữa lưu bàn thành collection riêng hay nhúng vào Restaurant, cuối cùng chọn nhúng cho đơn giản vì số bàn ít - nhưng phải sửa lại schema đã lỡ viết.
- Lỗi quên `.save()` sau khi đổi qrSecret làm mình tưởng logic revoke sai, dò một hồi mới thấy là chưa ghi xuống DB.
- Có hai khái niệm "bàn" dễ lẫn: bàn gắn QR và bàn trên sơ đồ tầng. Phải đặt tên rõ (`tables` vs `floor-tables`) để mình với FE khỏi nhầm.

## Bài học rút ra

- QR là điểm nhạy cảm về bảo mật nên làm revoke ngay từ đầu là đúng, đỡ phải chắp vá sau.
- Với Mongo, nhúng hay tách tùy vào cách truy vấn và khối lượng dữ liệu, không có công thức cứng - lần này nhúng hợp lý hơn.
- Đặt tên rõ ràng cho các khái niệm gần giống nhau giúp cả nhóm bớt hiểu lầm khi ghép API.

## Kế hoạch tuần 9

- Module Menu: menu có phiên bản (draft -> published -> archived).
- Menu items: thêm/sửa/xóa món, phân loại, giá, trạng thái.
- Allergen tagging: gắn nhãn dị ứng cho từng món (14 loại theo chuẩn EU).

## Nhận xét cuối tuần

Tuần này bắt đầu ra hình hài: đã có nhà hàng, bàn và QR - những thứ FE render lên nhìn thấy được nên làm cũng có động lực hơn. Việc vừa code vừa ngồi khớp với bạn FE giúp mình để ý hơn tới việc đặt tên field và giữ response nhất quán.
