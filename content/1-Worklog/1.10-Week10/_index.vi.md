---
title: "Worklog Tuần 10"
date: 2026-07-06
weight: 10
chapter: false
pre: " <b> 1.10. </b> "
---

## Thông tin chung

| Nội dung      | Chi tiết                                                        |
| ------------- | -------------------------------------------------------------- |
| Thời gian     | 06/07/2026 - 12/07/2026                                        |
| Tuần thực tập | Tuần 10                                                        |
| Giai đoạn     | SmartMenu - Session khách, xem menu public và đặt món          |
| Vai trò       | Full-stack, phụ trách backend; FE có hỗ trợ từ thành viên nhóm |
| Chủ đề chính  | Guest session qua QR, public menu view, orders + status pipeline |

## Định hướng tuần 10

Tuần này làm phần dành cho **khách** - nửa còn lại của sản phẩm. Khách quét QR trên bàn để mở một session (không cần đăng ký tài khoản), xem menu published, khai báo dị ứng để hệ thống cảnh báo món hợp/không hợp, rồi đặt món. Phía owner thì nhận đơn và đẩy trạng thái đơn theo một luồng cố định. Đây là lúc mấy module rời của các tuần trước bắt đầu nối vào nhau.

## Mục tiêu tuần 10

- Guest session: tạo session bằng quét QR (verify qrSecret), tự hết hạn khi không hoạt động.
- Khai báo dị ứng/khẩu vị gắn theo session.
- Public menu view: trả menu published kèm nhãn match dị ứng (đỏ/vàng/xanh).
- Orders: khách đặt món, owner quản lý đơn theo pipeline `pending -> ... -> completed`.

## Nội dung thực hiện trong tuần

### Ngày 1 - Thứ hai, 06/07/2026

Tạo guest session.

- Thiết kế model `Session`: restaurantId, tableNumber, allergens, preferences, trạng thái, thời điểm hết hạn.
- Viết `POST /sessions`: nhận restaurantId + tableNumber + qrSecret, verify secret khớp với bàn rồi mới tạo session.
- Đây là chỗ nối với QR tuần 8: nếu owner đã revoke thì secret cũ verify fail, không tạo được session.

```bash
curl -X POST http://localhost:3000/api/v1/sessions \
  -H "Content-Type: application/json" \
  -d '{"restaurantId":"'"$RESTAURANT_ID"'","tableNumber":5,"qrSecret":"'"$QR_SECRET"'"}'
```

### Ngày 2 - Thứ ba, 07/07/2026

Session hết hạn + khai báo dị ứng.

- Thêm logic session tự hết hạn sau một khoảng không hoạt động (lưu `expiresAt`, check khi dùng).
- Viết `PATCH /sessions/:sessionId/allergens` để khách khai dị ứng và khẩu vị.
- Cân nhắc dùng TTL index của Mongo cho hết hạn, nhưng tạm check thủ công theo `expiresAt` cho dễ kiểm soát, note lại để tối ưu sau.

### Ngày 3 - Thứ tư, 08/07/2026

Public menu view + nhãn dị ứng.

- Viết `GET /public/restaurants/:restaurantId/menu?sessionId=...&lang=vi`: trả menu published + items.
- Logic nhãn match: đối chiếu allergen của món với allergen khách khai trong session -> gắn nhãn đỏ (chứa chất khách dị ứng), vàng (có thể chứa), xanh (an toàn).
- Đây là phần mình thấy hay nhất: dữ liệu allergen tuần 9 giờ có chỗ dùng thật.

Có bug: khi session chưa khai dị ứng thì tất cả món ra nhãn xanh - đúng ý, nhưng lúc đầu mình để null gây crash. Thêm mặc định mảng rỗng là ổn.

### Ngày 4 - Thứ năm, 09/07/2026

Đặt món (guest) + model Order.

- Thiết kế model `Order`: sessionId, danh sách items (menuItemId, quantity, notes), customerNotes, status, restaurantId.
- Viết `POST /orders` cho khách (không cần auth, scope theo sessionId).
- Kiểm tra: món đặt phải thuộc menu đang published và đang `available`.

```bash
curl -X POST http://localhost:3000/api/v1/orders \
  -H "Content-Type: application/json" \
  -d '{"sessionId":"'"$SESSION_ID"'","items":[{"menuItemId":"'"$ITEM_ID"'","quantity":2,"notes":"Ít hành"}],"customerNotes":"Cay nhiều"}'
```

### Ngày 5 - Thứ sáu, 10/07/2026

Status pipeline + quản lý đơn phía owner.

- Chốt pipeline một chiều: `pending -> confirmed -> preparing -> ready -> served -> completed`, hoặc `cancelled`.
- Viết `PATCH /orders/:orderId/status` cho owner, chặn nhảy lùi hoặc nhảy cóc trạng thái.
- Viết `GET /orders` (owner xem đơn nhà hàng) và `GET /orders/session/:sessionId` (khách poll đơn của mình).

Ban đầu mình cho đổi status tự do, sau thấy nguy hiểm (đơn completed lại quay về pending) nên viết bảng chuyển trạng thái hợp lệ, chỉ cho đi tới.

### Ngày 6 - Thứ bảy, 11/07/2026

Ghép FE tablet + owner.

- Nối app tablet (màn hình khách gọi món) với luồng session -> menu -> order.
- Nối app owner với màn hình danh sách đơn và nút đổi trạng thái.
- Sửa vài chỗ format thời gian và tên trạng thái cho khớp i18n bên FE.
- Test thử end-to-end một vòng: quét QR -> xem menu -> đặt món -> owner đẩy trạng thái -> khách thấy cập nhật.

## Kết quả đạt được trong tuần

- Khách tạo được session qua QR, có verify secret và hết hạn.
- Khai báo dị ứng và xem menu public kèm nhãn cảnh báo đỏ/vàng/xanh.
- Đặt món và theo dõi đơn theo session.
- Owner quản lý đơn theo pipeline một chiều, có kiểm soát chuyển trạng thái.
- Chạy được một vòng end-to-end giữa tablet, owner và backend.

## Khó khăn gặp phải

- Logic nhãn dị ứng lúc session chưa khai báo bị crash vì để null; sửa bằng mặc định mảng rỗng.
- Pipeline trạng thái nếu để tự do rất dễ loạn dữ liệu, phải viết bảng chuyển hợp lệ mới yên tâm.
- Việc test end-to-end cần nhiều biến (restaurantId, qrSecret, sessionId, itemId) nên mình viết một script nhỏ set biến cho dễ gõ lại.

## Bài học rút ra

- Dữ liệu làm ở tuần trước (allergen) tới giờ mới "sống" - cho thấy thiết kế sớm mà đúng thì về sau ráp vào rất mượt.
- Trạng thái nghiệp vụ nên ràng buộc chặt hướng đi, không nên tin phía gọi API sẽ đổi đúng.
- Có một luồng end-to-end chạy được sớm giúp mình và FE phát hiện lệch hợp đồng API nhanh hơn nhiều.

## Kế hoạch tuần 11

- Cash payment: đánh dấu các đơn mở của session là completed, ghi nhận Payment.
- Payments: liệt kê, phân trang, refund.
- Reservations và Operating Hours.

## Nhận xét cuối tuần

Tuần này sản phẩm chạy được "một vòng" thật sự nên khá phấn khích. Nhìn khách quét QR rồi món hiện lên phía owner, mình mới thấy công của mấy tuần dựng nền lộ rõ. Vẫn còn thanh toán và đặt bàn để làm cho đủ nghiệp vụ.
