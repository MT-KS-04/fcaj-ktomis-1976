---
title: "Worklog Tuần 7"
date: 2026-06-15
weight: 7
chapter: false
pre: " <b> 1.7. </b> "
---

### Mục tiêu Tuần 7:

- Khởi động dự án **SmartMenu** - hệ thống menu số & đặt món cho nhà hàng qua QR.
- Chốt kiến trúc, tech stack và thiết kế schema cơ sở dữ liệu.
- Hoàn thành module Authentication cho chủ nhà hàng.
- Vai trò: Full-stack, phụ trách toàn bộ backend; frontend có hỗ trợ từ thành viên nhóm.

### Các công việc thực hiện trong tuần:

| Ngày | Công việc                                                                                                                                                                                                                                                                                                                     | Ngày bắt đầu | Ngày hoàn thành | Tài liệu tham khảo                           |
| ---- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------ | --------------- | -------------------------------------------- |
| 2    | - Họp nhóm chốt phạm vi MVP của dự án <br> - Chốt tech stack backend: <br>&emsp; + Node.js + TypeScript <br>&emsp; + Express <br>&emsp; + MongoDB (Mongoose) <br> - **Thực hành:** <br>&emsp; + Dựng cấu trúc thư mục project <br>&emsp; + Cài đặt dependencies, cấu hình nodemon + ts-node <br>&emsp; + Dựng route `/health` | 15/06/2026   | 15/06/2026      | <https://github.com/MT-KS-04/smart-menu-api> |
| 3    | - Thiết kế schema cơ sở dữ liệu: <br>&emsp; + Owner, Restaurant <br>&emsp; + Menu, MenuItem <br>&emsp; + Order, Session, Token <br> - **Thực hành:** <br>&emsp; + Viết `lib/mongoose.ts` kết nối MongoDB <br>&emsp; + Dựng model Owner với index unique cho email <br>&emsp; + Cấu hình TypeScript path alias                 | 16/06/2026   | 16/06/2026      | <https://github.com/MT-KS-04/smart-menu-api> |
| 4    | - Xây dựng luồng đăng ký (register): <br>&emsp; + Validate input bằng express-validator <br>&emsp; + Hash password bằng bcryptjs <br> - **Thực hành:** <br>&emsp; + Viết controller register <br>&emsp; + Dựng middleware xử lý lỗi validation <br>&emsp; + Test API bằng curl                                                | 17/06/2026   | 17/06/2026      | <https://github.com/MT-KS-04/smart-menu-api> |
| 5    | - Xây dựng luồng đăng nhập (login) và JWT: <br>&emsp; + Access token ngắn hạn <br>&emsp; + Refresh token trong httpOnly cookie <br> - **Thực hành:** <br>&emsp; + Viết controller login <br>&emsp; + Viết `lib/jwt.ts` gom hàm ký/verify token                                                                                | 18/06/2026   | 18/06/2026      | <https://github.com/MT-KS-04/smart-menu-api> |
| 6    | - Xây dựng refresh token, logout và middleware auth: <br>&emsp; + Lưu refresh token vào collection Token để thu hồi <br>&emsp; + Middleware `authenticate` verify Bearer token <br> - **Thực hành:** <br>&emsp; + Viết route refresh-token và logout <br>&emsp; + Cấu hình cookie-parser                                      | 19/06/2026   | 19/06/2026      | <https://github.com/MT-KS-04/smart-menu-api> |
| 7    | - Chuẩn hóa response và bảo mật cơ bản: <br>&emsp; + Gom hàm success/error <br>&emsp; + Thêm helmet, cors, compression <br> - Thống nhất hợp đồng API với thành viên làm frontend <br> - **Thực hành:** <br>&emsp; + Ghi file `.env.example`                                                                                  | 20/06/2026   | 20/06/2026      | <https://github.com/MT-KS-04/smart-menu-fe>  |

### Kết quả đạt được Tuần 7:

- Chốt được kiến trúc và tech stack cho dự án SmartMenu:
  - Backend: Node.js, TypeScript, Express, MongoDB (Mongoose)
  - Frontend: React 18, Vite, Tailwind, MUI (do thành viên nhóm phụ trách UI)
  - Lý do chọn MongoDB: dữ liệu menu/đơn linh hoạt, phù hợp giai đoạn đầu

- Dựng xong skeleton backend chạy được với cấu trúc rõ ràng:
  - config, controller/v1, router/v1
  - model, middleware
  - lib, utils

- Thiết kế được các collection cốt lõi trong MongoDB:
  - Owner, Restaurant
  - Menu, MenuItem
  - Order, Session, Token

- Hoàn thành module Authentication đầy đủ:
  - Đăng ký với validate input và hash password bằng bcryptjs
  - Đăng nhập và cấp JWT access token
  - Refresh token lưu trong httpOnly cookie, có thể thu hồi
  - Logout thu hồi refresh token

- Xây dựng được các thành phần dùng chung cho các module sau:
  - Middleware `authenticate` xác thực Bearer token
  - Middleware xử lý lỗi tập trung
  - Hàm chuẩn hóa response success/error
  - Bảo mật cơ bản với helmet, cors, compression

- Thống nhất được hợp đồng API với frontend về base URL, format token và luồng đăng nhập.
