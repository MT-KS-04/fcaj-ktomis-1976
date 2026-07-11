---
title: "Chia sẻ, đóng góp ý kiến"
date: 2024-01-01
weight: 7
chapter: false
pre: " <b> 7. </b> "
---

> Vài chia sẻ và cảm nhận của mình sau khi tham gia chương trình First Cloud AI Journey và làm project cuối kỳ cùng nhóm.

Trong suốt chương trình, mình đi từ những tuần học nền tảng về AWS cho tới lúc bắt tay ghép mọi thứ lại thành một project chạy được thật. Nhờ đó mình hiểu rõ hơn về cloud, kiến trúc serverless và cách một ứng dụng thực tế được dựng lên rồi vận hành trên AWS. Dưới đây là vài đánh giá cá nhân của mình.

### Đánh giá chung

**1. Môi trường học tập và làm việc**
Môi trường trong chương trình khá hợp với sinh viên mới tìm hiểu về cloud. Nội dung đi từ dễ tới khó, học nền tảng trước rồi mới tới thực hành và làm project nên không bị ngợp. Mình thích chỗ được chủ động: tự đọc tài liệu, tự làm theo từng bước và ghi lại lỗi gặp phải, nhờ vậy mà quen dần với việc tự học và tự xử lý vấn đề. Nếu có thêm vài buổi trao đổi nhóm định kỳ để mọi người chia sẻ tiến độ và hỏi han nhau thì mình nghĩ sẽ còn tốt hơn.

**2. Sự hỗ trợ của mentor / team admin**
Mentor và team admin hỗ trợ khá tốt, hướng dẫn rõ ràng nên dễ theo. Điều mình quý là khi mình kẹt lỗi trên Console hay CLI, mọi người thường gợi ý hướng để mình tự tìm ra nguyên nhân chứ không đưa đáp án luôn. Hơi cực nhưng nhờ vậy mình hiểu sâu hơn và rèn được tư duy tự gỡ lỗi, thay vì làm theo một cách máy móc.

**3. Sự phù hợp giữa công việc và chuyên ngành học**
Nội dung khá sát với ngành công nghệ thông tin của mình. Mấy thứ như backend, API, cơ sở dữ liệu, xác thực người dùng, lưu trữ file hay triển khai hệ thống đều liên quan trực tiếp tới những gì mình học trên trường. Riêng project cuối kỳ giúp mình đem được nhiều kiến thức rời rạc vào một chỗ: dựng API backend, làm việc với database NoSQL, nối frontend với backend, xử lý upload file và tích hợp các dịch vụ cloud lại với nhau.

**4. Cơ hội học hỏi và phát triển kỹ năng**
Về kỹ thuật, mình được thực hành thật với nhiều dịch vụ: S3 để lưu file, Lambda cho phần xử lý backend, API Gateway để dựng REST API, DynamoDB lưu dữ liệu, Cognito cho đăng nhập, và Secrets Manager để giấu thông tin nhạy cảm thay vì nhét vào code. CloudWatch thì gần như lúc nào cũng mở để dò log khi có lỗi. Về kỹ năng mềm, mình thấy mình khá lên ở khoản tự học, làm việc nhóm, viết báo cáo và nhất là bình tĩnh phân tích lỗi thay vì cuống lên như hồi đầu.

**5. Văn hóa và tinh thần đồng đội**
Làm project nhóm mới thấy chia việc rõ ràng quan trọng cỡ nào. Mỗi người ôm một mảng - frontend, backend, phần AI, deploy, testing - rồi phải khớp lại với nhau. Khi một chỗ hỏng, cả nhóm xúm vào dò cùng cho ra nguyên nhân. Qua đó mình hiểu một hệ thống hoàn chỉnh không phải công của riêng ai, mà là nhiều mảnh ghép phải ăn khớp.

---

### Một số câu hỏi khác

**Điều mình hài lòng nhất**
Hài lòng nhất là được tự tay dựng và nhìn hệ thống của mình chạy trơn từ đầu tới cuối. Trước đây mình chỉ biết cloud ở mức lý thuyết, làm xong project mới thật sự hiểu các dịch vụ AWS nối vào nhau ra sao để thành một hệ thống hoàn chỉnh. Cảm giác lúc mọi thứ ăn khớp và chạy được khá đã.

**Điều mình nghĩ chương trình nên cải thiện**
Mình nghĩ chương trình có thể thêm vài thứ để người mới dễ vớt:

- Buổi định hướng ban đầu về cách đọc tài liệu AWS cho khỏi lạc.
- Sơ đồ kiến trúc mẫu cho từng loại project để dễ hình dung trước khi làm.
- Một danh sách lỗi hay gặp như AccessDenied, CORS, Lambda timeout kèm cách xử lý.
- Buổi review giữa kỳ để soi lại tiến độ project.
- Checklist dọn tài nguyên sau khi xong để tránh quên rồi phát sinh chi phí.

**Nếu giới thiệu cho bạn bè, mình có khuyên tham gia không?**
Có. Ai muốn tìm hiểu AWS, serverless và cách dựng một project thật thì đây là bước đệm tốt, vừa có nền tảng vừa có project để đưa vào portfolio. Chỉ có điều mình sẽ dặn trước là phải chuẩn bị tinh thần tự học nhiều, vì AWS rộng và lỗi đôi khi khó hiểu nếu chưa quen.

---

### Đề xuất và mong muốn

Một vài đề xuất nhỏ để trải nghiệm mượt hơn: roadmap rõ theo từng tuần, thêm tài liệu giải thích kiến trúc bằng hình, checklist setup môi trường và checklist bảo mật trước khi làm project, cùng với buổi hỏi đáp định kỳ với mentor.

Về phần mình, sau project này mình muốn đào sâu thêm về serverless best practices, bảo mật API với Cognito, Secrets Manager, event-driven với SQS, CI/CD trên AWS và cách tối ưu chi phí khi chạy hệ thống thật.

### Kết luận

Nhìn lại, đây là quãng thời gian đáng với mình. Từ chỗ chỉ biết cloud trên giấy, giờ mình đã tự dựng được một hệ thống thật trên AWS và hiểu từng mảnh trong đó làm gì. Dù vẫn còn vài điểm có thể tốt hơn, chương trình đã cho mình cái nhìn thực tế về cách làm việc và cách một project công nghệ được ráp lại. Mình cảm ơn mentor, team admin và chương trình đã tạo điều kiện để mình học, thực hành và hoàn thành project cùng nhóm. Nếu có dịp mình vẫn muốn theo cộng đồng tiếp và phụ được gì cho các bạn khóa sau thì phụ.