---
title: "Worklog Tuần 7"
date: 2026-06-14
weight: 7
chapter: false
pre: " <b> 1.7. </b> "
---

## Thông tin chung

| Nội dung         | Chi tiết                                                                     |
| ---------------- | ---------------------------------------------------------------------------- |
| Thời gian        | 14/06/2026 - 20/06/2026                                                      |
| Tuần thực tập    | Tuần 7                                                                       |
| Giai đoạn        | Bắt đầu project SmartMenu - Khởi tạo & Authentication                        |
| Dự án            | SmartMenu (hệ thống menu số & đặt món cho nhà hàng qua QR)                   |
| Vai trò          | Full-stack, phụ trách toàn bộ backend; frontend có hỗ trợ từ thành viên nhóm |
| Chủ đề chính     | Lên kiến trúc, thiết kế schema, dựng skeleton API và module auth             |

## Định hướng tuần 7

Bắt đầu từ tuần này nhóm mình chuyển từ giai đoạn học sang làm project thật: **SmartMenu** - hệ thống cho phép chủ nhà hàng quản lý menu, bàn, đơn hàng; còn khách quét QR trên bàn để xem menu và gọi món mà không cần tài khoản. Mình nhận phần backend nên tuần đầu tập trung dựng nền: chốt stack, kiến trúc thư mục, thiết kế schema và làm xong module authentication cho chủ nhà hàng.

Frontend do một bạn trong nhóm lo phần UI, mình chủ yếu thống nhất luồng dữ liệu và hợp đồng API để hai bên khớp nhau.

## Mục tiêu tuần 7

- Chốt tech stack và dựng skeleton project backend.
- Thiết kế sơ bộ các collection trong MongoDB.
- Làm module auth: register, login, JWT access token + refresh token.
- Dựng middleware xác thực và xử lý lỗi tập trung.

## Nội dung thực hiện trong tuần

### Ngày 1 - Thứ hai, 15/06/2026

Chốt hướng đi và dựng khung project.

- Họp nhóm chốt phạm vi MVP: chủ nhà hàng quản lý menu/đơn, khách quét QR gọi món.
- Chốt stack backend: Node.js + TypeScript + Express + MongoDB (Mongoose). Lý do chọn Mongo là dữ liệu menu/đơn khá linh hoạt, dễ phải migrate schema liên tục ở giai đoạn đầu.
- `npm init`, dựng cấu trúc thư mục: `config`, `controller/v1`, `router/v1`, `model`, `middleware`, `lib`, `utils`.
- Cài `express`, `mongoose`, `dotenv`, set up `nodemon` + `ts-node` để chạy dev.

Cuối ngày dựng được server chạy `npm run dev` lên `http://localhost:3000/api/v1` với route `/health` trả về ok.

### Ngày 2 - Thứ ba, 16/06/2026

Thiết kế schema và kết nối database.

- Phác các collection chính trên giấy trước: `Owner`, `Restaurant`, `Menu`, `MenuItem`, `Order`, `Session`, `Token`. Mấy cái còn lại (Payment, Reservation, FloorTable) để tuần sau khi làm tới.
- Viết `lib/mongoose.ts` kết nối Mongo qua `MONGOOSE_URL`, log trạng thái connect bằng winston.
- Dựng model `Owner` với email + passwordHash, thêm index unique cho email.

Có vướng chỗ TypeScript path alias (`@/...`) chạy không ra, phải thêm `tsconfig-paths` vào nodemon mới import gọn được thay vì `../../..`.

### Ngày 3 - Thứ tư, 17/06/2026

Làm luồng đăng ký.

- Viết controller `register`: validate email/password bằng `express-validator`, hash password bằng `bcryptjs` rồi lưu Owner.
- Dựng middleware bắt lỗi validation trả về format thống nhất.
- Test bằng curl:

```bash
curl -X POST http://localhost:3000/api/v1/auth/register \
  -H "Content-Type: application/json" \
  -d '{"email":"owner@example.com","password":"Password123!"}'
```

Lần đầu quên `await` lúc hash password nên field `passwordHash` lưu vào là một Promise, đọc ra thấy `[object Promise]` mới tá hỏa. Thêm `await` là xong.

### Ngày 4 - Thứ năm, 18/06/2026

Làm luồng đăng nhập + JWT.

- Viết controller `login`: tìm owner theo email, so password bằng `bcrypt.compare`, ký access token bằng `jsonwebtoken`.
- Chốt cơ chế 2 token: access token ngắn hạn trả trong response, refresh token dài hạn set vào httpOnly cookie cho an toàn.
- Viết `lib/jwt.ts` gom hàm ký/verify cho gọn.

```bash
curl -X POST http://localhost:3000/api/v1/auth/login \
  -c cookies.txt \
  -H "Content-Type: application/json" \
  -d '{"email":"owner@example.com","password":"Password123!"}'
```

### Ngày 5 - Thứ sáu, 19/06/2026

Refresh token + logout + middleware auth.

- Lưu refresh token vào collection `Token` để có thể thu hồi (logout thì xóa).
- Viết route `refresh-token`: đọc cookie, verify, cấp access token mới.
- Viết middleware `authenticate`: đọc header `Authorization: Bearer`, verify access token, gắn `ownerId` vào request.
- Route `logout` thu hồi refresh token hiện tại.

Có lúc refresh hoài báo lỗi, hóa ra do quên `cookie-parser` nên `req.cookies` undefined. Thêm middleware là chạy.

### Ngày 6 - Thứ bảy, 20/06/2026

Dọn dẹp và thống nhất với frontend.

- Chuẩn hóa response trả về (`utils` gom hàm success/error) để FE parse cho dễ.
- Thêm `helmet`, `cors`, `compression` vào app.
- Ngồi với bạn làm FE thống nhất base URL, format token và luồng login để bạn ghép vào app owner.
- Ghi lại các biến môi trường vào `.env.example`.

## Kết quả đạt được trong tuần

- Dựng xong skeleton backend chạy được, có `/health`.
- Kết nối MongoDB và thiết kế xong các schema cốt lõi đợt đầu.
- Hoàn thành module auth: register, login, refresh token, logout.
- Có middleware auth và xử lý lỗi dùng chung cho các module sau.

## Khó khăn gặp phải

- Path alias TypeScript làm mình mất thời gian đầu tuần, import cồng kềnh hoài tới khi thêm `tsconfig-paths`.
- Vụ quên `await` khi hash password dùng kiểu lỗi ngớ ngẩn mà debug lâu, vì nhìn code không thấy sai, chỉ khi in ra DB mới thấy `[object Promise]`.
- Refresh token lỗi vì thiếu `cookie-parser` - nhắc mình là mấy middleware nhỏ mà thiếu là gãy cả luồng.

## Bài học rút ra

- Chịu khó phác schema ra giấy trước khi code đỡ phải sửa tới sửa lui, dù Mongo linh hoạt thật.
- Tách token thành access ngắn + refresh trong httpOnly cookie tuy làm nhiều hơn nhưng an toàn, đáng để đầu tư từ đầu.
- Thống nhất hợp đồng API với FE sớm giúp sau này đỡ phải sửa qua sửa lại vì hai bên hiểu khác nhau.

## Kế hoạch tuần 8

- Làm module Restaurant: mỗi owner một nhà hàng, tự sinh bàn + QR code theo `tableCount`.
- Làm chức năng lấy và thu hồi (revoke) QR của từng bàn.
- Bắt đầu module Floor Tables (sơ đồ bàn theo tầng/khu vực).

## Nhận xét cuối tuần

Tuần đầu của project chủ yếu là dựng nền nên chưa có tính năng "nhìn thấy được", nhưng phần auth và cấu trúc làm chắc thì các module sau ráp vào sẽ nhanh. Mình thấy làm project thật khác học ở chỗ phải nghĩ trước về việc mở rộng, chứ không chỉ code cho chạy.
