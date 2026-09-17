---
title: "Worklog Tuần 12"
date: "2026-10-05"
weight: 12
chapter: false
pre: "<b> 1.12 </b>"
---


### Mục tiêu tuần 12:

* Tìm hiểu Amazon Elastic IP và cách sử dụng địa chỉ IP tĩnh cho máy chủ EC2.
* Nghiên cứu cách tổ chức Security Group giữa Application Load Balancer và các EC2 trong Target Group.
* Tìm hiểu cách sử dụng IAM Role để cấp quyền cho EC2 truy cập các dịch vụ AWS mà không cần lưu Access Key trên máy chủ.
* Nghiên cứu Amazon CloudWatch Agent, CloudWatch Logs, Log Group và Log Stream để thu thập log từ nhiều EC2.
* Tìm hiểu các tính năng của Amazon S3 phục vụ lưu trữ bản sao dữ liệu như Block Public Access, mã hóa, Versioning và Lifecycle Rule.
* Tổng hợp các dịch vụ AWS cần thiết và xây dựng kế hoạch triển khai hạ tầng dự án theo từng giai đoạn.

### Các công việc cần triển khai trong tuần này:

| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --------- | ------------ | --------------- | -------------- |
| 2 | Tìm hiểu Elastic IP, cách cấp phát, liên kết và giải phóng địa chỉ IP trên EC2 | 05/10/2026 | 05/10/2026 | https://docs.aws.amazon.com/AWSEC2/ |
| 3 | Nghiên cứu Security Group cho ALB và EC2, nguyên tắc chỉ cho phép lưu lượng cần thiết giữa các thành phần | 06/10/2026 | 06/10/2026 | https://docs.aws.amazon.com/elasticloadbalancing/ |
| 4 | Tìm hiểu IAM Role, Instance Profile và nguyên tắc phân quyền tối thiểu cho EC2 | 07/10/2026 | 07/10/2026 | https://docs.aws.amazon.com/IAM/ |
| 5 | Nghiên cứu CloudWatch Agent và cách tổ chức Log Group, Log Stream cho nhiều EC2 | 08/10/2026 | 08/10/2026 | https://docs.aws.amazon.com/AmazonCloudWatch/ |
| 6 | Tìm hiểu Block Public Access, mã hóa, Versioning và Lifecycle Rule trên Amazon S3 | 09/10/2026 | 09/10/2026 | https://docs.aws.amazon.com/s3/ |
| 7 | Tổng hợp kiến thức và lập kế hoạch áp dụng các dịch vụ AWS vào từng giai đoạn của dự án | 10/10/2026 | 10/10/2026 | https://docs.aws.amazon.com/ |

### Kết quả đạt được tuần 12:

* Hiểu được vai trò, cách liên kết và các lưu ý chi phí khi sử dụng Elastic IP với EC2.
* Xác định được nguyên tắc cấu hình Security Group để ALB có thể chuyển request đến EC2 mà không mở rộng cổng truy cập không cần thiết.
* Hiểu cách IAM Role cung cấp thông tin xác thực tạm thời cho EC2 và giảm rủi ro so với việc lưu Access Key dài hạn.
* Nắm được cách CloudWatch Agent gửi log từ nhiều EC2 vào CloudWatch Logs và cách phân biệt nguồn log bằng Log Stream.
* Hiểu cách bảo vệ và quản lý vòng đời bản sao dữ liệu trên S3 bằng Block Public Access, mã hóa, Versioning và Lifecycle Rule.
* Hoàn thành tài liệu tổng hợp và kế hoạch áp dụng các dịch vụ AWS cho những tuần triển khai dự án tiếp theo.
