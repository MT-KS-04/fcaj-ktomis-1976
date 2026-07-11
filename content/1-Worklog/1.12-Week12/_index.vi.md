---
title: "Worklog Tuần 12"
date: 2026-07-09
weight: 12
chapter: false
pre: " <b> 1.12. </b> "
---

## Thông tin chung

| Nội dung      | Chi tiết                                                        |
| ------------- | -------------------------------------------------------------- |
| Thời gian     | 19/07/2026 - 25/07/2026                                        |
| Tuần thực tập | Tuần 12                                                        |
| Giai đoạn     | SmartMenu - Hoàn thiện, bảo mật, test và demo                  |
| Vai trò       | Full-stack, phụ trách backend; FE có hỗ trợ từ thành viên nhóm |
| Chủ đề chính  | Rate limit, rà phân quyền, viết test, ghép FE, chuẩn bị demo   |

## Định hướng tuần 12

Tuần cuối của giai đoạn này mình không thêm tính năng lớn nữa mà tập trung làm cho hệ thống **chắc và an toàn**: thêm rate limit, rà lỗi phân quyền các route owner, viết test cho luồng chính, dọn code và ghép nốt frontend để chuẩn bị demo. Đây là phần ít "hào nhoáng" nhưng quyết định sản phẩm có dùng được thật hay không.

## Mục tiêu tuần 12

- Thêm rate limit và soát lỗi bảo mật cơ bản.
- Rà toàn bộ route owner đảm bảo đúng phân quyền.
- Viết test cho auth, order và một vài luồng quan trọng.
- Ghép nốt FE, dọn code, chuẩn bị demo và tài liệu.

## Nội dung thực hiện trong tuần

### Ngày 1 - Thứ hai, 20/07/2026

Rà soát bảo mật.

- Thêm `express-rate-limit` cho các route nhạy cảm (login, register) để tránh brute force.
- Soát lại header bảo mật với `helmet`, cấu hình `cors` cho đúng origin của owner/tablet/landing thay vì để `*`.
- Đọc lại toàn bộ route xem có chỗ nào quên middleware `authenticate` không.

Phát hiện một route floor-tables lỡ để lọt không check quyền, ai có token cũng sửa được bàn nhà hàng khác - sửa lại thêm kiểm tra ownerId.

### Ngày 2 - Thứ ba, 21/07/2026

Phân quyền và kiểm tra sở hữu.

- Thống nhất nguyên tắc: mọi thao tác trên tài nguyên của nhà hàng đều phải kiểm tra tài nguyên đó thuộc về owner đang đăng nhập.
- Viết một helper kiểm tra sở hữu dùng chung cho menu, order, reservation, payment, floor-table thay vì lặp lại code check ở từng controller.
- Test thử: dùng token của owner A gọi sửa menu của owner B -> phải bị chặn 403.

### Ngày 3 - Thứ tư, 22/07/2026

Viết test.

- Set up Vitest/Jest cho backend, viết test cho auth (register/login sai mật khẩu, refresh token).
- Viết test cho luồng order: đặt món hợp lệ, đặt món đã sold_out phải fail, đổi trạng thái nhảy cóc phải fail.
- Chạy test thấy vài chỗ trả status code chưa nhất quán (400 vs 422), chỉnh lại cho đồng bộ.

### Ngày 4 - Thứ năm, 23/07/2026

Dọn code và log.

- Rà lại logger winston/morgan, bỏ mấy `console.log` còn sót lúc debug.
- Chuẩn hóa message lỗi trả về cho FE, gom mã lỗi vào một chỗ.
- Format toàn bộ bằng Prettier, sửa mấy cảnh báo type còn lại của TypeScript.

### Ngày 5 - Thứ sáu, 24/07/2026

Ghép nốt FE và chạy thử toàn hệ thống.

- Ngồi với bạn FE rà lại toàn bộ 3 app (owner, tablet, landing) gọi đúng API thật thay vì mock.
- Sửa vài lỗi CORS khi FE gọi từ origin khác, và vài chỗ field lệch tên giữa type FE và response BE.
- Chạy thử kịch bản đầy đủ: owner tạo nhà hàng -> soạn menu -> publish -> khách quét QR -> gọi món -> owner xử lý đơn -> thanh toán -> xem lại payment.

### Ngày 6 - Thứ bảy, 25/07/2026

Chuẩn bị demo và tổng kết.

- Viết lại README backend: mô tả, hướng dẫn chạy, biến môi trường, danh sách endpoint kèm ví dụ curl.
- Chuẩn bị data demo sạch để buổi trình bày chạy mượt.
- Tổng kết lại toàn bộ những gì đã làm trong 6 tuần project, note các phần còn để dành (AI gợi ý allergen, realtime cho đơn, tối ưu session bằng TTL index).

## Kết quả đạt được trong tuần

- Thêm rate limit, siết CORS và vá lỗ hổng phân quyền floor-tables.
- Có helper kiểm tra sở hữu dùng chung, phân quyền nhất quán toàn hệ thống.
- Có bộ test cho auth và order, chuẩn hóa status code.
- 3 app FE chạy với backend thật, hoàn tất kịch bản demo end-to-end.
- README và data demo sẵn sàng.

## Khó khăn gặp phải

- Lỗ hổng phân quyền ở floor-tables suýt lọt - nhắc mình phải rà quyền toàn bộ chứ không tin là "chắc đã check rồi".
- Status code trả về không nhất quán làm test fail lắt nhắt, phải thống nhất lại quy ước từ đầu.
- Ghép FE với backend thật lòi ra mấy chỗ lệch tên field mà lúc dùng mock không thấy.

## Bài học rút ra

- Bảo mật và phân quyền phải rà có hệ thống; một route quên check là dễ thành lỗ hổng.
- Viết test tuy mất thời gian nhưng giúp phát hiện mấy chỗ không nhất quán mà đọc code thường bỏ qua.
- Mock API tiện cho FE làm song song, nhưng phải sớm test với backend thật để lòi ra khác biệt.

## Tổng kết giai đoạn project (Tuần 7-12)

Sau 6 tuần, nhóm mình hoàn thành phần lớn MVP của SmartMenu. Về backend (phần mình phụ trách trọn vẹn), mình đã tự làm từ đầu tới cuối: auth cho owner, quản lý nhà hàng và QR bàn, menu có phiên bản và allergen tagging, session khách qua QR, đặt món với pipeline trạng thái, thanh toán và refund, đặt bàn, giờ hoạt động, cùng các route public cho khách. Frontend có bạn trong nhóm hỗ trợ phần UI của 3 app (owner, tablet, landing), mình phối hợp về hợp đồng API và ghép nối.

Những phần để dành cho sau: cho AI gợi ý allergen từ mô tả món, cập nhật đơn realtime thay vì để khách poll, và tối ưu vòng đời session.

## Nhận xét cuối tuần

Khép lại giai đoạn project, mình thấy tự tin hơn hẳn so với lúc mới học xong lý thuyết. Làm trọn phần backend của một hệ thống thật cho mình hiểu cảm giác từ lúc lên ý tưởng, thiết kế dữ liệu, code, sửa tới sửa lui rồi ráp với frontend và lo cả bảo mật. Việc phối hợp với bạn FE cũng dạy mình cách làm việc nhóm cho khớp thay vì mạnh ai nấy làm.
