---
title: "Cấu hình IAM và giám sát log PM2 với CloudWatch"
date: "2026-09-14"
weight: 3
chapter: false
pre: "<b> 5.3 </b>"
---

## Tổng quan

Trong chương này, chúng ta sẽ thực hiện **cấu hình IAM và Amazon CloudWatch Logs** để thu thập và theo dõi log của backend đang chạy bằng **PM2 trên Amazon EC2**.

Amazon CloudWatch Logs là dịch vụ lưu trữ và tra cứu log trên nền tảng AWS. Dịch vụ này giúp chúng ta kiểm tra hoạt động của backend, tìm thông báo lỗi và hỗ trợ xử lý sự cố mà không cần kết nối SSH mỗi lần xem log.

Trong quá trình triển khai, chúng ta sẽ thực hiện các nội dung chính sau:

- Tạo **IAM role** cấp quyền cho EC2 gửi log đến CloudWatch.
- Gắn IAM role vào **EC2 Instance** đang chạy backend.
- Cài đặt và cấu hình **Amazon CloudWatch Agent** trên EC2.
- Thu thập log đầu ra và log lỗi của tiến trình **PM2**.
- Kiểm tra và tra cứu log trên **CloudWatch Logs**.

---

## Kiến trúc triển khai

Trong mô hình này, **Amazon EC2** tiếp tục đóng vai trò là máy chủ chạy backend. **PM2** quản lý tiến trình ứng dụng và ghi log đầu ra (`stdout`) cùng log lỗi (`stderr`) vào các file trên máy chủ.

**Amazon CloudWatch Agent** được cài đặt trên EC2 để đọc các file log của PM2 và gửi nội dung đến **CloudWatch Logs**. Đường dẫn file log cần được xác định theo đúng user đang chạy PM2.

**IAM role** được gắn vào EC2 để cấp quyền cho CloudWatch Agent gửi log bằng thông tin xác thực tạm thời. Các thành phần trong kiến trúc có vai trò như sau:

- **EC2 Instance:** Chạy backend và lưu các file log của ứng dụng.
- **PM2:** Quản lý tiến trình backend và ghi log stdout, stderr.
- **IAM role:** Cấp quyền truy cập AWS cần thiết cho CloudWatch Agent.
- **CloudWatch Agent:** Thu thập log trên EC2 và gửi đến CloudWatch Logs.
- **CloudWatch Logs:** Tập trung log trong log group và log stream để theo dõi, tìm kiếm và xử lý sự cố.

Luồng thu thập log của ứng dụng:

```text
Backend → PM2 → File log trên EC2 → CloudWatch Agent → CloudWatch Logs
                                         ↑
                                  IAM role của EC2
```

Log được tổ chức trong một **log group** dành cho backend và các **log stream** phân biệt theo instance, loại log. EC2 cần có kết nối HTTPS đến CloudWatch Logs trong Region sử dụng để gửi dữ liệu.

---

## Nội dung thực hiện

Quá trình cấu hình IAM và thu thập log PM2 trên EC2 được chia thành các bước sau:

1. [Tạo IAM role](5.3.1-create_roleiam/)
2. [Gắn IAM role cho EC2](5.3.2-attachiamrole/)
3. [Cấu hình cloudwatch agennt cho EC2](5.3.3-configurepm2logs/)
