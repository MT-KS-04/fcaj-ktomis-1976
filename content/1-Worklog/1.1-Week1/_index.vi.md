---
title: "Worklog Tuần 1"
date: 2026-05-03
weight: 1
chapter: false
pre: " <b> 1.1. </b> "
---

## Thông tin chung

| Nội dung         | Chi tiết                                                                                 |
| ---------------- | ---------------------------------------------------------------------------------------- |
| Thời gian        | 03/05/2026 - 09/05/2026                                                                  |
| Tuần thực tập    | Tuần 1                                                                                   |
| Giai đoạn        | Explore AWS Services                                                                     |
| Chương trình học | First Cloud Journey                                                                      |
| Chủ đề chính     | Khởi tạo tài khoản, quản lý chi phí, phân quyền IAM và hạ tầng mạng - tính toán nền tảng |
| Mục tiêu tuần    | Tạo và bảo mật tài khoản AWS, nắm AWS Budgets, AWS Support, IAM, VPC, EC2, S3 và AWS CLI |

## Định hướng học tập Tuần 1

Đây là tuần đầu tiên của kỳ thực tập tại chương trình **Workforce Bootcamp - First Cloud AI Journey**, học theo lộ trình **First Cloud Journey** ở phần **Explore AWS Services**. Tuần này em bắt đầu từ những workshop nền tảng và dễ tiếp cận nhất: tạo tài khoản AWS, quản lý chi phí, tìm kiếm hỗ trợ, phân quyền IAM, sau đó đọc tiếp sang phần mạng (VPC), máy chủ ảo (EC2) và lưu trữ (S3).

Vì mới bắt đầu nên em ưu tiên đọc kỹ tài liệu và làm theo hướng dẫn từng bước ở mức thử nghiệm, chủ yếu để hiểu bản chất chứ chưa dựng gì hoàn chỉnh. Mỗi ngày em chỉ tập trung 1–2 dịch vụ để không bị quá tải.

## Mục tiêu học tập Tuần 1

- Tạo AWS Account và bật bảo mật cơ bản (MFA cho root account).
- Quản lý chi phí với AWS Budgets.
- Tìm hiểu cách nhận hỗ trợ qua AWS Support.
- Phân quyền truy cập với AWS IAM (User, Group, Role, Policy).
- Tìm hiểu hạ tầng mạng với Amazon VPC.
- Tìm hiểu máy chủ ảo với Amazon EC2 và IAM Roles for EC2.
- Thao tác dòng lệnh với AWS CLI.
- Tìm hiểu static website hosting với Amazon S3.

## Nội dung thực hiện trong tuần

### Ngày 1 - Thứ hai, 04/05/2026

Chủ đề: **Creating Your First AWS Account** và **Managing Costs with AWS Budgets**.

Nội dung đã thực hiện:

- Đọc workshop Creating Your First AWS Account và tự tạo tài khoản AWS Free Tier theo hướng dẫn.
- Bật MFA cho root account theo các bước trong bài.
- Đọc phần AWS Budgets, làm thử một budget nhỏ để xem cơ chế cảnh báo chi phí qua email hoạt động thế nào.

Kết quả đạt được:

- Có tài khoản AWS để dùng cho cả kỳ, đã bật MFA.
- Hiểu cách AWS Budgets cảnh báo khi chi phí vượt ngưỡng.

### Ngày 2 - Thứ ba, 05/05/2026

Chủ đề: **Getting Help with AWS Support** và **Access Management with AWS IAM**.

Nội dung đã thực hiện:

- Đọc về các gói AWS Support và xem quy trình tạo một support case.
- Đọc tài liệu IAM để phân biệt User, Group, Role, Policy.
- Tìm hiểu nguyên tắc least privilege và đọc thử vài IAM Policy dạng JSON để quen cấu trúc.
- Làm theo hướng dẫn tạo một IAM User có quyền hạn chế thay cho việc dùng root.

Kết quả đạt được:

- Biết khi cần thì tìm hỗ trợ ở đâu và ở mức nào.
- Nắm được vai trò của từng thành phần IAM và cách tạo User, gán Policy cơ bản.

### Ngày 3 - Thứ tư, 06/05/2026

Chủ đề: **Networking Essentials with Amazon VPC**.

Nội dung đã thực hiện:

- Đọc tài liệu VPC: CIDR block, subnet, phân biệt public và private subnet.
- Tìm hiểu Route Table, Internet Gateway, NAT Gateway.
- Tìm hiểu sự khác nhau giữa Security Group và Network ACL.
- Làm theo workshop dựng thử một VPC có public và private subnet để hình dung cách các thành phần nối với nhau.

Kết quả đạt được:

- Hình dung được cấu trúc một VPC cơ bản.
- Phân biệt được Security Group (stateful) và Network ACL (stateless), ít nhất là trên lý thuyết.

### Ngày 4 - Thứ năm, 07/05/2026

Chủ đề: **Compute Essentials with Amazon EC2**.

Nội dung đã thực hiện:

- Đọc về EC2: AMI, instance type, key pair, EBS volume.
- Làm theo hướng dẫn tạo thử một EC2 instance Free Tier trong public subnet đã dựng hôm trước.
- Thử SSH vào instance và chạy vài lệnh để kiểm tra.

Kết quả đạt được:

- Hiểu được vai trò của AMI, instance type và key pair khi tạo máy ảo.
- Kết nối được vào instance vừa tạo để xem nó chạy thế nào.

### Ngày 5 - Thứ sáu, 08/05/2026

Chủ đề: **Instance Profiling with IAM Roles for EC2** và **Command Line Operations with AWS CLI**.

Nội dung đã thực hiện:

- Đọc về IAM Role gắn cho EC2 (instance profile) và lý do không nên lưu Access Key trực tiếp trên máy chủ.
- Làm theo bài hướng dẫn gán một Role cho EC2 rồi thử kiểm tra quyền.
- Cài AWS CLI trên máy cá nhân, cấu hình Access Key, Secret Key, Region.
- Gõ thử vài lệnh cơ bản để làm quen.

Sau khi cấu hình xong, em kiểm tra xem đã đăng nhập đúng tài khoản chưa:

```bash
aws sts get-caller-identity
```

```json
{
  "UserId": "AIDA********EXAMPLE",
  "Account": "123456789012",
  "Arn": "arn:aws:iam::123456789012:user/intern-dev"
}
```

Lúc đầu em quên chưa `aws configure` mà gõ luôn lệnh trên nên bị:

```
Unable to locate credentials. You can configure credentials by running "aws configure".
```

Chạy `aws configure` nhập lại Access Key / Secret Key / Region (ap-southeast-1) thì mới ổn. Sau đó thử liệt kê region để chắc CLI gọi được API:

```bash
aws ec2 describe-regions --query "Regions[].RegionName" --output text
```

Kết quả đạt được:

- Hiểu tại sao dùng Role cho EC2 an toàn hơn.
- Dùng được AWS CLI cho vài thao tác đơn giản, thấy nó nhanh hơn Console ở một số việc.
- Nhớ được lệnh `aws sts get-caller-identity` để lần sau kiểm tra nhanh mình đang dùng account/role nào — cái này sau chắc dùng nhiều.

### Ngày 6 - Thứ bảy, 09/05/2026

Chủ đề: **Static Website Hosting with Amazon S3**.

Nội dung đã thực hiện:

- Đọc về S3: bucket, object, storage class.
- Làm theo workshop tạo một bucket, upload file và bật static website hosting.
- Tìm hiểu bucket policy và tùy chọn block public access.

Phần này em làm thử cả trên CLI cho quen. Tạo bucket và upload file index:

```bash
aws s3 mb s3://intern-static-demo-2026
aws s3 cp index.html s3://intern-static-demo-2026/
```

```
make_bucket: intern-static-demo-2026
upload: ./index.html to s3://intern-static-demo-2026/index.html
```

Bật static website hosting:

```bash
aws s3 website s3://intern-static-demo-2026/ --index-document index.html
```

Lúc mở endpoint website lần đầu em bị `403 Forbidden`, mất một lúc mới hiểu là do Block Public Access đang bật và chưa có bucket policy cho phép đọc công khai. Sau khi tắt block ở mức bucket và thêm policy `s3:GetObject` cho `Principal: "*"` thì trang mới hiện.

Kết quả đạt được:

- Tạo được bucket và cho hiển thị một trang tĩnh đơn giản theo hướng dẫn.
- Hiểu bucket policy ảnh hưởng thế nào tới việc file có công khai hay không.
- Nhớ được bộ lệnh `s3 mb` / `s3 cp` / `s3 website` để lần sau khỏi phải bấm Console.

## Tổng kết kiến thức Tuần 1

| Nhóm kiến thức | Nội dung đã học                                          |
| -------------- | -------------------------------------------------------- |
| Account & Cost | AWS Account, MFA, AWS Budgets                            |
| Support        | AWS Support                                              |
| Security       | IAM User, Group, Role, Policy, least privilege           |
| Networking     | VPC, Subnet, Route Table, IGW, NAT, Security Group, NACL |
| Compute        | EC2, AMI, instance type, IAM Roles for EC2               |
| CLI            | AWS CLI                                                  |
| Storage        | S3, static website hosting, bucket policy                |

## Kết quả đạt được trong tuần

- Có tài khoản AWS đã bật MFA và một budget cảnh báo chi phí.
- Nắm cơ bản IAM và tạo được User, gán Policy theo least privilege.
- Làm theo được workshop dựng VPC và EC2 ở mức thử.
- Dùng được IAM Role cho EC2 và vài lệnh AWS CLI.
- Cho chạy được một trang tĩnh trên S3 theo hướng dẫn.

## Khó khăn gặp phải

- IAM Policy viết bằng JSON lúc đầu nhìn khá rối, em phải đọc đi đọc lại mới quen được ba phần Effect, Action, Resource.
- Có lần thử SSH vào EC2 mà không vào được, loay hoay một lúc mới nhận ra là do rule inbound trong Security Group và route table chưa đúng.
- Phần bucket policy của S3 hơi khó, em bị Access Denied vài lần vì chưa hiểu rõ block public access hoạt động ra sao.
- Lúc mới cài AWS CLI em gõ lệnh luôn mà quên `aws configure`, nó báo "Unable to locate credentials" làm em tưởng cài hỏng, chạy lại configure là xong.

## Bài học rút ra

- Em thấy rõ là không nên đụng vào root account cho việc hàng ngày, tạo IAM User riêng vừa an toàn vừa gọn.
- Mấy thứ như MFA hay budget nên bật ngay từ đầu, để sau dễ quên mà lại phát sinh chi phí.
- Đọc lý thuyết thôi chưa đủ, lúc tự bấm theo workshop mới thấy nhiều chỗ mình tưởng hiểu mà thật ra chưa.

## Kế hoạch cho Tuần 2

- Tìm hiểu Amazon RDS (cơ sở dữ liệu quan hệ).
- Tìm hiểu Amazon Lightsail và Lightsail Containers.
- Tìm hiểu EC2 Auto Scaling và Amazon CloudWatch.
- Tìm hiểu Amazon Route 53 và AWS Cloud9.

## Nhận xét cuối tuần

Tuần đầu chủ yếu là làm quen, đọc tài liệu và bấm thử theo hướng dẫn nên chưa có gì phức tạp, nhưng nhờ vậy em có cái nền để tuần sau đỡ bỡ ngỡ. Đi từ mấy chủ đề dễ trước rồi mới tới VPC, EC2 giúp em không bị rối ngay từ đầu.
