---
title: "Worklog Tuần 9"
date: 2026-06-29
weight: 9
chapter: false
pre: " <b> 1.9. </b> "
---

### Mục tiêu Tuần 9:

- Xây dựng module Menu có quản lý phiên bản (draft → published → archived).
- Xây dựng CRUD món ăn (MenuItem) với phân loại, giá và trạng thái.
- Xây dựng chức năng gắn nhãn dị ứng (allergen tagging) theo chuẩn 14 loại của EU.
- Song song: cấu hình S3 và Lambda để chuẩn bị triển khai dự án lên AWS.

### Các công việc thực hiện trong tuần:

| Ngày | Công việc                                                                                                                                                                                                                                                                                              | Ngày bắt đầu | Ngày hoàn thành | Tài liệu tham khảo                                                         |
| ---- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------ | --------------- | -------------------------------------------------------------------------- |
| 2    | - Thiết kế vòng đời menu: <br>&emsp; + `draft` → `published` → `archived` <br>&emsp; + Mỗi nhà hàng chỉ một menu published <br> - Thiết kế model Menu: name, imageUrl, status, version                                                                                                                 | 29/06/2026   | 29/06/2026      | <https://github.com/MT-KS-04/smart-menu-api>                               |
| 3    | - Xây dựng chức năng tạo và publish menu: <br>&emsp; + `POST /menus/upload` tạo menu draft <br>&emsp; + `POST /menus/:id/publish` tự archive menu cũ <br> - **Thực hành:** <br>&emsp; + Xử lý ràng buộc chỉ một menu published tại một thời điểm                                                       | 30/06/2026   | 30/06/2026      | <https://github.com/MT-KS-04/smart-menu-api>                               |
| 4    | - Xây dựng CRUD menu và menu item: <br>&emsp; + `GET /menus`, `PATCH`, `DELETE` <br>&emsp; + Model MenuItem: nameVi, price, category, descVi, status <br> - **Thực hành:** <br>&emsp; + Viết `POST /menus/:id/items` và `GET /menus/:id/items`                                                         | 01/07/2026   | 01/07/2026      | <https://github.com/MT-KS-04/smart-menu-api>                               |
| 5    | - Hoàn thiện sửa/xóa món ăn: <br>&emsp; + Đổi giá, trạng thái (available / sold_out) <br>&emsp; + Thêm data mẫu để frontend render thử <br> - **AWS:** <br>&emsp; + Tạo S3 bucket chứa bản build frontend <br>&emsp; + Cấu hình IAM policy cấp quyền truy cập S3                                       | 02/07/2026   | 02/07/2026      | <https://000057.awsstudygroup.com> <br> <https://000002.awsstudygroup.com> |
| 6    | - Xây dựng chức năng allergen tagging: <br>&emsp; + Chốt 14 loại dị ứng chuẩn EU vào constants <br>&emsp; + Mức độ: contains / may_contain <br>&emsp; + Cờ `verified` (owner xác nhận) <br> - **Thực hành:** <br>&emsp; + Viết `PATCH /menus/:id/items/:itemId/allergens`                              | 03/07/2026   | 03/07/2026      | <https://github.com/MT-KS-04/smart-menu-api>                               |
| 7    | - Rà soát validation và sửa lỗi: <br>&emsp; + Giá không âm, category không rỗng <br>&emsp; + Allergen phải nằm trong 14 loại cho phép <br>&emsp; + Xử lý item mồ côi khi xóa menu <br> - **AWS:** <br>&emsp; + Deploy thử backend qua Lambda Function URL <br>&emsp; + Kiểm tra API hoạt động trên AWS | 04/07/2026   | 04/07/2026      | <https://000022.awsstudygroup.com>                                         |

### Kết quả đạt được Tuần 9:

- Hoàn thành module Menu với quản lý phiên bản:
  - Vòng đời rõ ràng: draft (đang soạn) → published (khách xem) → archived (menu cũ)
  - Publish menu mới tự động archive menu đang published
  - Đảm bảo ràng buộc chỉ một menu published tại một thời điểm
  - Menu cũ được lưu lại thay vì bị ghi đè

- Hoàn thành CRUD món ăn (MenuItem):
  - Thêm, sửa, xóa món
  - Quản lý theo tên, giá, phân loại (category), mô tả
  - Đổi trạng thái available / sold_out

- Hoàn thành chức năng gắn nhãn dị ứng (allergen tagging):
  - Chuẩn hóa 14 loại dị ứng theo chuẩn EU vào constants dùng chung
  - Phân biệt mức độ: contains (chứa) và may_contain (có thể chứa)
  - Cờ `verified` để owner xác nhận
  - Ràng buộc allergen phải nằm trong danh sách cho phép

- Nắm được kinh nghiệm khi làm việc với MongoDB:
  - Không có ràng buộc khóa ngoại như SQL nên phải tự dọn quan hệ khi xóa
  - Tách data dùng chung ra constants để frontend và backend nhất quán

- Bước đầu triển khai dự án lên AWS:
  - Tạo S3 bucket để chứa bản build frontend
  - Cấu hình IAM policy cấp quyền truy cập S3 (`s3:ListBucket` trên bucket ARN, các action object-level trên `/*` ARN)
  - Deploy thử backend qua Lambda Function URL và kiểm tra API hoạt động
