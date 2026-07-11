---
title: "Worklog Tuần 11"
date: 2026-07-09
weight: 11
chapter: false
pre: " <b> 1.11. </b> "
---

## Thông tin chung

| Nội dung      | Chi tiết                                                       |
| ------------- | -------------------------------------------------------------- |
| Thời gian     | 12/07/2026 - 18/07/2026                                        |
| Tuần thực tập | Tuần 11                                                        |
| Giai đoạn     | SmartMenu - Thanh toán, đặt bàn và giờ hoạt động               |
| Vai trò       | Full-stack, phụ trách backend; FE có hỗ trợ từ thành viên nhóm |
| Chủ đề chính  | Cash payment, Payments + refund, Reservations, Operating Hours |

## Định hướng tuần 11

Sản phẩm đã chạy được vòng gọi món, tuần này mình bù nốt các nghiệp vụ còn thiếu để nó giống một hệ thống nhà hàng thật: thanh toán tiền mặt và lưu lịch sử thanh toán (kèm refund), đặt bàn (cả owner tạo lẫn khách tự đặt), và giờ mở/đóng cửa theo từng ngày trong tuần. Mấy phần này không quá khó về kỹ thuật nhưng nhiều ràng buộc nghiệp vụ nên phải cẩn thận.

## Mục tiêu tuần 11

- Cash payment: chốt tất cả đơn đang mở của một session, ghi nhận một Payment.
- Payments: liệt kê/phân trang, refund một payment đã completed.
- Reservations: owner tạo/liệt kê, đổi trạng thái; khách tự đặt qua route public.
- Operating Hours: cấu hình giờ mở/đóng theo từng ngày Mon-Sun.

## Nội dung thực hiện trong tuần

### Ngày 1 - Thứ hai, 13/07/2026

Thanh toán tiền mặt.

- Thiết kế model `Payment`: sessionId, restaurantId, tổng tiền, status (completed / refunded), thời điểm.
- Viết `POST /orders/session/:sessionId/cash-payment`: gom hết đơn đang mở của session, tính tổng, set các đơn thành completed và tạo một Payment.
- Đây là chỗ mình phải nghĩ về tính đúng: chỉ tính đơn chưa hủy, và một session thanh toán rồi không cho thanh toán lại.

```bash
curl -X POST http://localhost:3000/api/v1/orders/session/$SESSION_ID/cash-payment
```

### Ngày 2 - Thứ ba, 14/07/2026

Danh sách + phân trang payment.

- Viết `GET /payments` với filter theo status và phân trang (page, limit).
- Chuẩn hóa response phân trang (total, page, limit, data) để FE làm bảng cho dễ.
- Thêm ít data thanh toán mẫu để test phân trang không bị lệch khi qua trang 2.

### Ngày 3 - Thứ tư, 15/07/2026

Refund.

- Viết `POST /payments/:id/refund`: chỉ refund được payment đang `completed`, đổi sang `refunded`.
- Chặn refund hai lần: nếu đã refunded thì trả lỗi rõ ràng.
- Cân nhắc có nên "mở lại" đơn khi refund không, bàn với nhóm thì thống nhất MVP chỉ đánh dấu payment refunded, chưa đụng lại đơn - note lại để bàn sau.

### Ngày 4 - Thứ năm, 16/07/2026

Reservations (phía owner).

- Thiết kế model `Reservation`: customerName, customerPhone, time, partySize, tableNumber, notes, status.
- Pipeline: `pending -> confirmed -> seated -> completed`, hoặc `cancelled` / `no_show`.
- Viết `POST /reservations`, `GET /reservations` (filter status + phân trang), `PATCH /reservations/:id/status`.

```bash
curl -X POST http://localhost:3000/api/v1/reservations \
  -H "Authorization: Bearer $ACCESS_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{"customerName":"Nguyen Van A","customerPhone":"0987654321","time":"2026-07-20T18:30:00.000Z","partySize":4,"tableNumber":5}'
```

### Ngày 5 - Thứ sáu, 17/07/2026

Reservations (khách tự đặt) + Operating Hours.

- Viết route public `POST /public/restaurants/:restaurantId/reservations`: khách tự đặt, luôn tạo với status `pending` để owner duyệt.
- Thiết kế `OperatingHours`: mỗi ngày trong tuần có `isOpen`, `openTime`, `closeTime` dạng `HH:mm`.
- Viết `GET /operating-hours` và `PATCH /operating-hours` (cập nhật một hoặc nhiều ngày).

```bash
curl -X PATCH http://localhost:3000/api/v1/operating-hours \
  -H "Authorization: Bearer $ACCESS_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{"monday":{"isOpen":true,"openTime":"09:00","closeTime":"21:00"}}'
```

Có bug validate giờ: lúc đầu mình không check `openTime` phải trước `closeTime`, nhập ngược vẫn lưu. Thêm validate so sánh giờ.

### Ngày 6 - Thứ bảy, 18/07/2026

Route public còn lại + ghép FE.

- Thêm `GET /public/restaurants/:restaurantId/operating-hours` để landing/tablet hiển thị giờ mở cửa.
- Ghép FE: app owner làm màn hình payments (bảng + nút refund) và reservations; app landing làm form đặt bàn cho khách.
- Sửa vài chỗ định dạng ngày giờ và tiền cho khớp giữa BE và FE.

## Kết quả đạt được trong tuần

- Thanh toán tiền mặt gom đơn theo session, ghi nhận Payment.
- Liệt kê/phân trang payment và refund, chặn refund hai lần.
- Reservations đầy đủ: owner tạo/duyệt và khách tự đặt qua public.
- Operating Hours theo từng ngày, có validate giờ hợp lệ.
- FE ghép được các màn hình payments, reservations và form đặt bàn.

## Khó khăn gặp phải

- Cash payment phải cẩn thận tính đúng đơn (bỏ đơn hủy) và chặn thanh toán lại - logic nghiệp vụ nhiều hơn là kỹ thuật.
- Quên validate `openTime < closeTime` nên nhập ngược vẫn lưu, phải bổ sung check.
- Nhiều pipeline trạng thái (order, reservation) na ná nhau nên mình phải tách rõ từng băng chuyền để không dùng nhầm.

## Bài học rút ra

- Mấy nghiệp vụ "tưởng dễ" như thanh toán, đặt bàn lại lắm ràng buộc; code cho chạy thì nhanh nhưng cho đúng mới tốn công.
- Validate dữ liệu đầu vào (giờ, tiền, trạng thái) phải làm kỹ, vì lỗi kiểu nhập ngược giờ rất dễ lọt.
- Khi có nhiều pipeline giống nhau, tách bạch từng cái ngay từ đầu dễ nhẩm hơn là gộp chung cho "gọn".

## Kế hoạch tuần 12

- Rà soát bảo mật: rate limit, kiểm tra lại phân quyền các route owner.
- Viết test cho các luồng chính.
- Hoàn thiện, ghép nốt FE và chuẩn bị demo/triển khai.

## Nhận xét cuối tuần

Sau tuần này thì phần lớn nghiệp vụ đã đủ: gọi món, thanh toán, đặt bàn, giờ hoạt động. Backend gần như hoàn chỉnh, việc còn lại là soát bảo mật, viết test và làm cho mọi thứ chắc chắn hơn trước khi demo. Mình bắt đầu thấy dáng dấp một hệ thống thật chứ không còn là mấy API rời.
