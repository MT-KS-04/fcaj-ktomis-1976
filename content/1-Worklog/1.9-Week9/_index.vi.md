---
title: "Worklog Tuần 9"
date: 2026-06-28
weight: 9
chapter: false
pre: " <b> 1.9. </b> "
---

## Thông tin chung

| Nội dung      | Chi tiết                                                        |
| ------------- | -------------------------------------------------------------- |
| Thời gian     | 28/06/2026 - 04/07/2026                                        |
| Tuần thực tập | Tuần 9                                                         |
| Giai đoạn     | SmartMenu - Menu, món ăn và nhãn dị ứng                        |
| Vai trò       | Full-stack, phụ trách backend; FE có hỗ trợ từ thành viên nhóm |
| Chủ đề chính  | Menu có phiên bản, CRUD menu item, allergen tagging            |

## Định hướng tuần 9

Tuần này làm phần "ruột" của sản phẩm: menu và món ăn. Điểm mình đắn đo nhiều nhất là **quản lý phiên bản menu** - khi owner đổi menu thì menu cũ không nên biến mất mà nên được lưu lại, và chỉ một menu được "published" cho khách xem tại một thời điểm. Ngoài ra làm luôn phần gắn nhãn dị ứng cho món, vì đây là điểm ăn tiền của SmartMenu so với menu giấy thường.

## Mục tiêu tuần 9

- Model `Menu` với vòng đời draft -> published -> archived.
- Khi publish menu mới thì tự archive menu đang published.
- CRUD `MenuItem`: tên (vi), giá, category, mô tả, status.
- Allergen tagging: gắn danh sách nhãn dị ứng, mức độ (contains / may_contain), nguồn (AI gợi ý / owner xác nhận).

## Nội dung thực hiện trong tuần

### Ngày 1 - Thứ hai, 29/06/2026

Thiết kế vòng đời menu.

- Vẽ state của menu: `draft` (đang soạn) -> `published` (khách xem) -> `archived` (menu cũ).
- Thiết kế model `Menu`: name, imageUrl, status, restaurantId, version.
- Quyết định: mỗi nhà hàng nhiều menu nhưng chỉ một `published` tại một thời điểm.

### Ngày 2 - Thứ ba, 30/06/2026

Tạo menu + publish.

- Viết `POST /menus/upload` tạo menu mới ở trạng thái draft.
- Viết `POST /menus/:menuId/publish`: đặt menu này thành published, đồng thời tìm menu đang published trước đó archive lại.
- Đây là chỗ mình phải cẩn thận: nếu publish A trong khi B đang published mà quên archive B thì có 2 menu published cùng lúc. Viết lại thành thao tác 2 bước trong cùng luồng để tránh.

```bash
curl -X POST http://localhost:3000/api/v1/menus/$MENU_ID/publish \
  -H "Authorization: Bearer $ACCESS_TOKEN"
```

### Ngày 3 - Thứ tư, 01/07/2026

CRUD menu + item.

- Viết `GET /menus` (liệt kê mọi phiên bản), `PATCH /menus/:menuId`, `DELETE /menus/:menuId`.
- Model `MenuItem`: nameVi, price, category, descVi, status (available / sold_out), menuId.
- Viết `POST /menus/:menuId/items` và `GET /menus/:menuId/items`.

```bash
curl -X POST http://localhost:3000/api/v1/menus/$MENU_ID/items \
  -H "Authorization: Bearer $ACCESS_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{"nameVi":"Phở Bò","price":65000,"category":"Món chính","descVi":"Phở bò truyền thống","status":"available"}'
```

### Ngày 4 - Thứ năm, 02/07/2026

Sửa/xóa item + chỉnh data.

- Viết `PATCH /menus/:menuId/items/:itemId` (đổi giá/status/mô tả) và `DELETE`.
- Test đổi món sang `sold_out`:

```bash
curl -X PATCH http://localhost:3000/api/v1/menus/$MENU_ID/items/$ITEM_ID/status \
  -H "Authorization: Bearer $ACCESS_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{"price":70000,"status":"sold_out"}'
```

- Ngồi thêm ít data mẫu (mấy món phở, cơm, nước) để FE có cái render thử thay vì màn hình trắng.

### Ngày 5 - Thứ sáu, 03/07/2026

Allergen tagging.

- Chốt danh sách 14 loại dị ứng theo chuẩn EU (gluten, đậu phộng, sữa, trứng, hải sản...) đưa vào constants.
- Thiết kế: mỗi item có mảng `allergenTags`, mỗi tag gồm `allergen`, `confidence` (contains / may_contain), và cờ `verified` (owner đã xác nhận chưa).
- Viết `PATCH /menus/:menuId/items/:itemId/allergens`.

```bash
curl -X PATCH http://localhost:3000/api/v1/menus/$MENU_ID/items/$ITEM_ID/allergens \
  -H "Authorization: Bearer $ACCESS_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{"allergenTags":[{"allergen":"gluten","confidence":"contains"},{"allergen":"soy","confidence":"may_contain"}],"verified":true}'
```

Ý tưởng để dành: sau này có thể cho AI gợi ý allergen từ tên/mô tả món (nguồn = AI), rồi owner xác nhận (verified = true). Tuần này mình làm phần dữ liệu và API trước, chưa nối AI.

### Ngày 6 - Thứ bảy, 04/07/2026

Rà lỗi và ghép FE menu.

- Rà lỗi validation: giá không âm, category không rỗng, allergen phải nằm trong 14 loại cho phép.
- Sửa một bug: xóa menu mà chưa xóa item con, để lại item mồ côi. Thêm bước xóa item theo menuId khi xóa menu.
- Ghép với FE: bạn làm màn hình quản lý menu của app owner, mình chỉnh vài field tên cho khớp và bổ sung message lỗi rõ hơn.

## Kết quả đạt được trong tuần

- Menu có vòng đời draft/published/archived, publish tự archive menu cũ.
- CRUD menu và menu item đầy đủ.
- Allergen tagging với mức độ và cờ verified, ràng buộc trong 14 loại chuẩn.
- Có data mẫu để FE render và test.

## Khó khăn gặp phải

- Vụ "chỉ một menu published" làm mình phải viết cẩn thận, suýt để lọt trường hợp 2 menu published cùng lúc.
- Bug item mồ côi khi xóa menu - nhắc mình là Mongo không tự ràng buộc khóa ngoại như SQL, phải tự dọn quan hệ.
- Danh sách 14 allergen ban đầu mình gõ tay dễ sai chính tả, phải đưa vào constants dùng chung để FE và BE thống nhất.

## Bài học rút ra

- Quản lý phiên bản (versioning) tuy làm phức tạp hơn nhưng đúng nhu cầu thật của nhà hàng - không nên vì ngại mà cho sửa đè thẳng.
- Không có ràng buộc khóa ngoại thì mình phải tự lo tính toàn vẹn dữ liệu, nhất là lúc xóa.
- Tách data dùng chung (như danh sách allergen) ra constants giúp cả hệ thống nhất quán, đỡ lệch giữa FE và BE.

## Kế hoạch tuần 10

- Guest session: khách quét QR tạo session (không cần tài khoản), khai báo dị ứng.
- Public menu view: khách xem menu published kèm nhãn cảnh báo dị ứng (đỏ/vàng/xanh).
- Orders: khách đặt món, owner quản lý đơn theo pipeline trạng thái.

## Nhận xét cuối tuần

Đây là tuần nội dung nặng nhất tới giờ vì menu là trái tim của sản phẩm. Làm xong phần versioning và allergen mình thấy sản phẩm bắt đầu có "chất riêng" chứ không chỉ là CRUD thường. Phần AI gợi ý allergen mình note lại để làm sau khi luồng chính chạy ổn.
