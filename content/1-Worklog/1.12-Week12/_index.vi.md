---
title: "Worklog Tuần 12"
date: 2026-07-20
weight: 12
chapter: false
pre: " <b> 1.12. </b> "
---

### Mục tiêu Tuần 12:

- Tăng cường bảo mật: rate limit, rà soát phân quyền toàn bộ hệ thống.
- Viết test cho các luồng chính và dọn dẹp mã nguồn.
- Hoàn tất triển khai lên AWS và chuẩn bị demo dự án.

### Các công việc thực hiện trong tuần:

| Ngày | Công việc                                                                                                                                                                                                                                                                                   | Ngày bắt đầu | Ngày hoàn thành | Tài liệu tham khảo                           |
| ---- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------ | --------------- | -------------------------------------------- |
| 2    | - Rà soát bảo mật hệ thống: <br>&emsp; + Thêm express-rate-limit cho login/register <br>&emsp; + Cấu hình cors đúng origin thay vì `*` <br>&emsp; + Soát header bảo mật với helmet <br> - **Thực hành:** <br>&emsp; + Rà toàn bộ route kiểm tra middleware `authenticate`                   | 20/07/2026   | 20/07/2026      | <https://github.com/MT-KS-04/smart-menu-api> |
| 3    | - Chuẩn hóa phân quyền và kiểm tra sở hữu: <br>&emsp; + Mọi thao tác phải kiểm tra tài nguyên thuộc owner đang đăng nhập <br> - **Thực hành:** <br>&emsp; + Viết helper kiểm tra sở hữu dùng chung <br>&emsp; + Test token owner A gọi API của owner B phải bị chặn 403                     | 21/07/2026   | 21/07/2026      | <https://github.com/MT-KS-04/smart-menu-api> |
| 4    | - Viết test cho các luồng chính: <br>&emsp; + Auth: register, login sai mật khẩu, refresh token <br>&emsp; + Order: đặt món hợp lệ, đặt món sold_out, chuyển trạng thái nhảy cóc <br> - **Thực hành:** <br>&emsp; + Chuẩn hóa status code trả về                                            | 22/07/2026   | 22/07/2026      | <https://github.com/MT-KS-04/smart-menu-api> |
| 5    | - Dọn dẹp mã nguồn: <br>&emsp; + Rà logger winston/morgan, bỏ console.log <br>&emsp; + Gom mã lỗi vào một chỗ <br>&emsp; + Format bằng Prettier, sửa cảnh báo TypeScript <br> - **AWS:** <br>&emsp; + Cấu hình biến môi trường cho Lambda <br>&emsp; + Kiểm tra log và debug qua CloudWatch | 23/07/2026   | 23/07/2026      | <https://000008.awsstudygroup.com>           |
| 6    | - Phối hợp frontend chạy thử toàn hệ thống: <br>&emsp; + 3 app (owner, tablet, landing) gọi API thật thay vì mock <br>&emsp; + Sửa lỗi CORS và lệch tên field <br> - **AWS:** <br>&emsp; + Kiểm tra toàn bộ luồng trên CloudFront + S3 + Lambda                                             | 24/07/2026   | 24/07/2026      | <https://github.com/MT-KS-04/smart-menu-fe>  |
| 7    | - Chuẩn bị demo và tổng kết dự án: <br>&emsp; + Viết README: hướng dẫn chạy, biến môi trường, danh sách endpoint <br>&emsp; + Chuẩn bị data demo <br>&emsp; + Tổng kết và ghi chú các phần phát triển tiếp                                                                                  | 25/07/2026   | 25/07/2026      | <https://github.com/MT-KS-04/smart-menu-api> |

### Kết quả đạt được Tuần 12:

- Tăng cường bảo mật cho hệ thống:
  - Thêm rate limit cho các route nhạy cảm (login, register) chống brute force
  - Siết cấu hình CORS về đúng origin của từng app thay vì cho phép tất cả
  - Rà soát header bảo mật với helmet
  - Phát hiện và vá lỗ hổng phân quyền ở module floor-tables

- Chuẩn hóa phân quyền toàn hệ thống:
  - Thống nhất nguyên tắc: mọi thao tác phải kiểm tra tài nguyên thuộc owner đang đăng nhập
  - Viết helper kiểm tra sở hữu dùng chung cho menu, order, reservation, payment, floor-table
  - Xác minh token của owner này không thao tác được trên tài nguyên của owner khác

- Xây dựng bộ test cho các luồng quan trọng:
  - Test module auth: đăng ký, đăng nhập sai mật khẩu, refresh token
  - Test luồng order: đặt món hợp lệ, chặn đặt món sold_out, chặn chuyển trạng thái nhảy cóc
  - Chuẩn hóa status code trả về cho nhất quán

- Dọn dẹp và hoàn thiện mã nguồn:
  - Chuẩn hóa logging với winston/morgan
  - Gom mã lỗi và message vào một nơi
  - Format toàn bộ mã nguồn, xử lý cảnh báo TypeScript

- Hoàn tất triển khai dự án trên AWS:
  - Kiến trúc: CloudFront (CDN) + S3 (frontend) + Lambda Function URL (backend API)
  - Cấu hình biến môi trường cho Lambda
  - Kiểm tra log và debug qua CloudWatch
  - Chạy thành công toàn bộ luồng trên môi trường AWS

- Hoàn thành kịch bản demo end-to-end: owner tạo nhà hàng → soạn menu → publish → khách quét QR → gọi món → owner xử lý đơn → thanh toán → xem lại lịch sử.

- Tổng kết dự án SmartMenu sau 6 tuần:
  - Backend: hoàn thành toàn bộ (auth, restaurant, QR, menu versioning, allergen, session, order, payment, reservation, operating hours)
  - Frontend: phối hợp cùng thành viên nhóm hoàn thiện 3 app (owner, tablet, landing)
  - Các hướng phát triển tiếp: AI gợi ý allergen, cập nhật đơn realtime, tối ưu vòng đời session
