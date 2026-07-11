---
title: "Worklog Tuần 4"
date: 2026-05-24
weight: 4
chapter: false
pre: " <b> 4.1. </b> "
---

## Thông tin chung

| Nội dung         | Chi tiết                                                                          |
| ---------------- | --------------------------------------------------------------------------------- |
| Thời gian        | 24/05/2026 - 30/05/2026                                                           |
| Tuần thực tập    | Tuần 4                                                                            |
| Giai đoạn        | Migrate to AWS & Optimize - Operations                                            |
| Chương trình học | First Cloud Journey                                                               |
| Chủ đề chính     | Di chuyển máy chủ và cơ sở dữ liệu, disaster recovery, quản trị vận hành          |
| Mục tiêu tuần    | Nắm VM Import/Export, DMS + SCT, Elastic Disaster Recovery, Systems Manager, Tags |

## Định hướng học tập Tuần 4

Tuần 4 chuyển sang giai đoạn **Migrate to AWS** và bắt đầu phần **Optimize - Operations**. Nội dung xoay quanh các công cụ di chuyển máy chủ (VM Import/Export), di chuyển database (DMS + SCT), khôi phục sau thảm họa (Elastic Disaster Recovery), rồi tới các công cụ quản trị vận hành (Systems Manager, Session Manager, Tags & Resource Groups). Mấy phần migration và DR khá trừu tượng, khó dựng thử đầy đủ nên tuần này em nghiêng về đọc hiểu quy trình là chính, chỗ nào làm theo được thì làm.

## Mục tiêu học tập Tuần 4

- Tìm hiểu VM Migration with AWS VM Import/Export.
- Tìm hiểu Database Migration with AWS DMS and Schema Conversion Tool (SCT).
- Tìm hiểu Disaster Recovery with AWS Elastic Disaster Recovery.
- Tìm hiểu Systems Management with AWS Systems Manager.
- Tìm hiểu Remote Server Access with Systems Manager Session Manager.
- Tìm hiểu Resource Organization with Tags and Resource Groups.

## Nội dung thực hiện trong tuần

### Ngày 1 - Thứ hai, 25/05/2026

Chủ đề: **VM Migration with AWS VM Import/Export**.

Nội dung đã thực hiện:

- Đọc về VM Import/Export và cách đưa máy ảo có sẵn lên AWS.
- Tìm hiểu các định dạng VM được hỗ trợ và vai trò của S3, IAM Role trong quá trình import.
- Đọc kỹ workshop từng bước, hình dung quy trình import một image thành AMI (chủ yếu đọc vì không có máy ảo nguồn để làm thật).

Kết quả đạt được:

- Hiểu về mặt quy trình cách đưa một VM on-premise lên AWS.
- Biết import cần chuẩn bị gì về định dạng và quyền.

### Ngày 2 - Thứ ba, 26/05/2026

Chủ đề: **Database Migration with AWS DMS and Schema Conversion Tool (SCT)**.

Nội dung đã thực hiện:

- Đọc về DMS và phân biệt migration cùng loại (homogeneous) với khác loại (heterogeneous).
- Tìm hiểu vai trò của SCT khi chuyển schema giữa các engine khác nhau.
- Tìm hiểu chế độ full load và CDC.
- Làm theo hướng dẫn cấu hình thử một replication task cơ bản.

Kết quả đạt được:

- Hiểu DMS di chuyển dữ liệu thế nào và CDC giúp giảm downtime ra sao.
- Nắm được khi nào cần dùng thêm SCT.

### Ngày 3 - Thứ tư, 27/05/2026

Chủ đề: **Disaster Recovery with AWS Elastic Disaster Recovery**.

Nội dung đã thực hiện:

- Đọc về Elastic Disaster Recovery và hai khái niệm quan trọng RPO, RTO.
- Tìm hiểu cơ chế replication liên tục và quy trình failover/failback.
- Đọc workshop để hình dung cách thiết lập DR cho một máy chủ nguồn.

Kết quả đạt được:

- Hiểu DR để làm gì và vì sao RPO/RTO lại quyết định cách thiết kế.
- Nắm được luồng failover về mặt lý thuyết.

### Ngày 4 - Thứ năm, 28/05/2026

Chủ đề: **Systems Management with AWS Systems Manager**.

Nội dung đã thực hiện:

- Đọc về Systems Manager và các thành phần như Parameter Store, Run Command, Patch Manager, Inventory.
- Làm theo hướng dẫn thử quản lý một EC2 instance qua Systems Manager.
- Thử lưu và đọc một tham số trong Parameter Store.

Lưu một tham số rồi đọc lại bằng CLI:

```bash
aws ssm put-parameter --name "/intern/db-host" \
  --value "intern-db.internal" --type String

aws ssm get-parameter --name "/intern/db-host" \
  --query "Parameter.Value" --output text
```

```
intern-db.internal
```

Với thông tin nhạy cảm thì bài hướng dẫn dùng `--type SecureString`, lúc đọc phải thêm `--with-decryption` mới ra giá trị thật — lần đầu em quên nên nó trả về chuỗi đã mã hóa, nhìn tưởng lỗi.

Kết quả đạt được:

- Hiểu Systems Manager gom nhiều việc quản trị về một chỗ.
- Dùng thử được Parameter Store và Run Command ở mức cơ bản.
- Nhớ là đọc SecureString phải kèm `--with-decryption`.

### Ngày 5 - Thứ sáu, 29/05/2026

Chủ đề: **Remote Server Access with Systems Manager Session Manager**.

Nội dung đã thực hiện:

- Đọc về Session Manager và cách truy cập EC2 mà không cần SSH hay mở port 22.
- Tìm hiểu vai trò của IAM Role và SSM Agent.
- Làm theo hướng dẫn mở thử một phiên vào EC2 qua Session Manager.

Mở phiên bằng CLI (không cần key pair, không mở port 22):

```bash
aws ssm start-session --target i-0abc123def456
```

Lần đầu em chạy thì bị:

```
An error occurred (TargetNotConnected) when calling StartSession operation: i-0abc123def456 is not connected.
```

Kiểm tra lại mới thấy instance chưa gắn IAM Role có policy `AmazonSSMManagedInstanceCore`, nên SSM Agent không "trình diện" được. Gắn role vào, đợi một chút rồi chạy lại thì vào được terminal ngay trong trình duyệt / CLI.

Kết quả đạt được:

- Vào được instance mà không cần key pair hay mở port, thấy tiện và an toàn hơn SSH.
- Hiểu vì sao cách này bảo mật hơn.
- Nhớ điều kiện để Session Manager chạy: instance phải có role `AmazonSSMManagedInstanceCore` và SSM Agent hoạt động.

### Ngày 6 - Thứ bảy, 30/05/2026

Chủ đề: **Resource Organization with Tags and Resource Groups**.

Nội dung đã thực hiện:

- Đọc về tagging strategy và cách nhóm tài nguyên bằng Resource Groups.
- Tìm hiểu vai trò của tag trong phân bổ chi phí và quản trị.
- Làm thử: gắn tag cho vài tài nguyên rồi tạo một Resource Group theo tag.
- Tổng hợp kiến thức cả tuần.

Kết quả đạt được:

- Biết cách tổ chức tài nguyên gọn gàng hơn bằng tag.
- Tạo được một Resource Group đơn giản.

## Tổng kết kiến thức Tuần 4

| Nhóm kiến thức     | Nội dung đã học                               |
| ------------------ | --------------------------------------------- |
| Server Migration   | VM Import/Export                              |
| Database Migration | DMS, SCT, full load, CDC                      |
| Disaster Recovery  | Elastic Disaster Recovery, RPO, RTO, failover |
| Operations         | Systems Manager, Parameter Store, Run Command |
| Remote Access      | Session Manager                               |
| Organization       | Tags và Resource Groups                       |

## Kết quả đạt được trong tuần

- Hiểu quy trình di chuyển máy chủ và database lên AWS.
- Nắm được ý tưởng và các khái niệm cốt lõi của disaster recovery.
- Dùng thử được Systems Manager và Session Manager.
- Biết tổ chức tài nguyên bằng tag và Resource Group.

## Khó khăn gặp phải

- VM Import/Export với DR tuần này em thấy hơi "chay", vì không có hệ thống nguồn thật để di chuyển nên chủ yếu đọc quy trình, hình dung là chính chứ chưa làm được đầu cuối.
- Hai khái niệm RPO và RTO lúc đầu em cứ lẫn lộn, phải lấy ví dụ cụ thể "mất tối đa bao nhiêu dữ liệu" và "bao lâu thì phục hồi" mới tách bạch được.
- Session Manager em thử mãi không vào, sau kiểm ra thì thiếu IAM Role và SSM Agent chưa sẵn sàng.

## Bài học rút ra

- Em thấy mấy chủ đề migration và DR đọc thì dễ gật gù nhưng làm thật chắc còn nhiều thứ phát sinh, nên giờ chỉ dám nói là hiểu quy trình.
- DR không phải cứ bật là xong, mà phải xuất phát từ yêu cầu RPO/RTO cụ thể mới thiết kế đúng.
- Session Manager làm em thích, không phải mở port hay giữ key mà vẫn vào được máy — kiểu này về sau chắc dùng nhiều.

## Kế hoạch cho Tuần 5

- Tiếp tục Optimize - Operations: CloudFormation, AWS CDK, Service Quotas.
- Tìm hiểu Cost and Usage Management, EC2 Resource Optimization, VPC Flow Logs.

## Nhận xét cuối tuần

Tuần 4 nghiêng nhiều về đọc hiểu quy trình hơn là bấm tay, vì mấy phần migration và DR khó dựng thử đầy đủ trong môi trường học. Bù lại phần Systems Manager và Session Manager thì làm được và khá thực tế, em thấy sẽ dùng lại về sau.
