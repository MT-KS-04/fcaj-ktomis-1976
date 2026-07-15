---
title: "Worklog Tuần 5"
date: 2026-06-01
weight: 5
chapter: false
pre: " <b> 5.1. </b> "
---

## Thông tin chung

| Nội dung         | Chi tiết                                                                       |
| ---------------- | ------------------------------------------------------------------------------ |
| Thời gian        | 01/06/2026 - 07/06/2026                                                        |
| Tuần thực tập    | Tuần 5                                                                         |
| Giai đoạn        | Optimize - Operations & Cost Optimization                                      |
| Chương trình học | First Cloud Journey                                                            |
| Chủ đề chính     | Infrastructure as Code, quản lý quota, quản lý chi phí và tối ưu tài nguyên    |
| Mục tiêu tuần    | Nắm CloudFormation, AWS CDK, Service Quotas, Cost Management, EC2 Optimization |

## Định hướng học tập Tuần 5

Tuần 5 tiếp tục giai đoạn **Optimize** với hai mảng: **Infrastructure as Code** (CloudFormation, AWS CDK) và **chi phí - tối ưu tài nguyên** (Service Quotas, Cost and Usage Management, EC2 Resource Optimization, VPC Flow Logs). IaC là phần khó và mới với em nên hai ngày đầu tuần em dồn cho CloudFormation và CDK, mấy ngày sau nhẹ hơn với chi phí và giám sát.

## Mục tiêu học tập Tuần 5

- Tìm hiểu Infrastructure as Code with AWS CloudFormation.
- Tìm hiểu Cloud Development Kit (AWS CDK) Essentials.
- Tìm hiểu Managing Quotas with Service Quotas.
- Tìm hiểu Cost and Usage Management.
- Tìm hiểu Right-Sizing with EC2 Resource Optimization.
- Tìm hiểu Network Monitoring with VPC Flow Logs.

## Nội dung thực hiện trong tuần

### Ngày 1 - Thứ hai, 01/06/2026

Chủ đề: **Infrastructure as Code with AWS CloudFormation**.

Nội dung đã thực hiện:

- Đọc về khái niệm Infrastructure as Code và lý do nên dùng.
- Tìm hiểu cấu trúc template: Resources, Parameters, Outputs, khái niệm stack và change set.
- Làm theo workshop: sửa một template mẫu rồi deploy thử để xem nó tự tạo tài nguyên.

Deploy một stack từ file template:

```bash
aws cloudformation deploy \
  --template-file s3-bucket.yaml \
  --stack-name intern-demo-stack
```

Lần đầu em bị lỗi vì template thụt lề sai (YAML rất khó tính khoản này):

```
Template format error: [/Resources] 'null' values are not allowed in templates
```

Sửa lại indent cho đúng rồi deploy thì ra:

```
Successfully created/updated stack - intern-demo-stack
```

Kiểm tra tài nguyên stack tạo ra:

```bash
aws cloudformation describe-stack-resources \
  --stack-name intern-demo-stack \
  --query "StackResources[].ResourceType" --output text
```

Kết quả đạt được:

- Hiểu lợi ích của IaC so với bấm tay trên Console.
- Deploy thử được một stack đơn giản từ template.
- Nhớ là YAML của CloudFormation nhạy cảm với thụt lề, sai một chút là fail cả template.

### Ngày 2 - Thứ ba, 02/06/2026

Chủ đề: **Cloud Development Kit (AWS CDK) Essentials**.

Nội dung đã thực hiện:

- Đọc về CDK và cách viết hạ tầng bằng ngôn ngữ lập trình thay vì YAML/JSON.
- Tìm hiểu khái niệm construct, stack, app và so sánh với CloudFormation thuần.
- Làm theo hướng dẫn khởi tạo một CDK project và chạy synth ra template.

Khởi tạo project và synth ra CloudFormation:

```bash
cdk init app --language typescript
cdk synth
```

Đến bước deploy thì em bị chặn:

```
This stack uses assets, so the toolkit stack must be deployed to the environment (Run "cdk bootstrap ...")
```

Hóa ra account chưa được bootstrap. Chạy lệnh này một lần cho region đang dùng rồi mới deploy được:

```bash
cdk bootstrap aws://123456789012/ap-southeast-1
cdk deploy
```

Kết quả đạt được:

- Hiểu CDK giúp viết hạ tầng gọn và dễ tái sử dụng hơn.
- Chạy thử được vòng khởi tạo - synth - deploy ở mức cơ bản.
- Nhớ là account mới phải `cdk bootstrap` một lần trước khi deploy, không thì cứ bị chặn.

### Ngày 3 - Thứ tư, 03/06/2026

Chủ đề: **Managing Quotas with Service Quotas**.

Nội dung đã thực hiện:

- Đọc về Service Quotas và ý nghĩa của giới hạn dịch vụ.
- Tìm hiểu cách xem quota hiện tại và quy trình yêu cầu tăng.
- Vào thử màn hình Service Quotas để xem giới hạn của vài dịch vụ đang dùng.

Kết quả đạt được:

- Hiểu quota ảnh hưởng thế nào tới việc mở rộng hệ thống.
- Biết chỗ để kiểm tra và xin tăng quota khi cần.

### Ngày 4 - Thứ năm, 04/06/2026

Chủ đề: **Cost and Usage Management**.

Nội dung đã thực hiện:

- Đọc về cách theo dõi và phân tích chi phí, mức sử dụng.
- Tìm hiểu Cost Explorer và báo cáo Cost and Usage Report.
- Vào Cost Explorer xem thử biểu đồ chi phí và lọc theo tag.

Kết quả đạt được:

- Biết dùng Cost Explorer để nhìn xu hướng chi phí.
- Hiểu tag giúp phân bổ chi phí theo nhóm ra sao.

### Ngày 5 - Thứ sáu, 05/06/2026

Chủ đề: **Right-Sizing with EC2 Resource Optimization**.

Nội dung đã thực hiện:

- Đọc về khái niệm right-sizing và cách dựa vào metric để chọn instance type hợp lý.
- Tìm hiểu công cụ đưa ra khuyến nghị tối ưu.
- Xem thử metric của một instance để hiểu khi nào nên đổi kích thước.

Kết quả đạt được:

- Hiểu right-sizing giúp tiết kiệm mà vẫn đủ hiệu năng.
- Biết dựa vào số liệu để quyết định thay vì chọn instance theo cảm tính.

### Ngày 6 - Thứ bảy, 06/06/2026

Chủ đề: **Network Monitoring with VPC Flow Logs**.

Nội dung đã thực hiện:

- Đọc về VPC Flow Logs và cấu trúc một bản ghi.
- Làm theo hướng dẫn bật flow log đẩy sang CloudWatch Logs.
- Xem thử vài bản ghi để hiểu cách đọc, lọc theo ACCEPT/REJECT.
- Tổng hợp kiến thức cả tuần.

Kết quả đạt được:

- Bật được flow log và đọc được bản ghi cơ bản.
- Hiểu flow log dùng để chẩn đoán kết nối và kiểm tra bảo mật.

## Tổng kết kiến thức Tuần 5

| Nhóm kiến thức         | Nội dung đã học                                       |
| ---------------------- | ----------------------------------------------------- |
| Infrastructure as Code | CloudFormation (template, stack), AWS CDK (construct) |
| Quotas                 | Service Quotas                                        |
| Cost Management        | Cost and Usage Management, Cost Explorer              |
| Optimization           | EC2 Resource Optimization (right-sizing)              |
| Network Monitoring     | VPC Flow Logs                                         |

## Kết quả đạt được trong tuần

- Deploy thử được hạ tầng bằng CloudFormation và CDK.
- Biết kiểm tra Service Quotas.
- Xem và phân tích được chi phí qua Cost Explorer.
- Hiểu cách right-sizing tài nguyên EC2.
- Bật và đọc được VPC Flow Logs.

## Khó khăn gặp phải

- CloudFormation template lúc đầu em nhìn cú pháp thấy nản, phải bắt đầu từ file mẫu rồi sửa dần từng khối chứ không viết mới nổi.
- CDK cần cài đặt và bootstrap môi trường, em vướng ở khâu này một lúc, chạy lệnh cứ báo lỗi tới khi làm đúng theo hướng dẫn.
- Flow log ra rất nhiều dòng, nhìn hoa cả mắt, em phải lọc theo REJECT và IP cần quan tâm thì mới thấy được cái mình muốn.

## Bài học rút ra

- Học IaC xong em mới thấy dựng tay trên Console tuy nhanh nhưng khó lặp lại, viết thành code thì lần sau tạo lại y hệt được.
- CDK hợp với em hơn vì viết bằng ngôn ngữ lập trình quen thuộc, đỡ phải nhớ cú pháp YAML.
- Chuyện tối ưu chi phí không chỉ là nhìn hóa đơn, mà gắn với tag, right-sizing và cả việc chịu khó xem số liệu.

## Kế hoạch cho Tuần 6

- Chuyển sang phần Optimize - Security: IAM Permission Boundaries, IAM Policies and Conditions.
- Tìm hiểu KMS, Secrets Manager, AWS WAF, Security Hub.

## Nhận xét cuối tuần

Tuần 5 phần IaC làm em mất sức nhất, nhưng cũng là phần em thấy đáng học nhất vì đổi hẳn cách nghĩ về dựng hạ tầng. Mấy phần chi phí và giám sát nhẹ hơn, coi như để cân bằng lại sau hai ngày đầu khá căng.
