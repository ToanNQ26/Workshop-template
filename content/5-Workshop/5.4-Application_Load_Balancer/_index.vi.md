---
title: "Cấu hình Application Load Balancer"
date: "2026-09-14"
weight: 4
chapter: false
pre: "<b> 5.4 </b>"
---

## Tổng quan

Trong chương này, chúng ta cấu hình **Application Load Balancer (ALB)** để tiếp nhận yêu cầu và chuyển đến backend website truyện tranh trên Amazon EC2. Khi có nhiều EC2 cùng chạy ứng dụng, ALB giúp **phân phối lưu lượng** và chuyển yêu cầu đến EC2 khỏe mạnh nếu một EC2 gặp lỗi.

## Kiến trúc triển khai

Người dùng truy cập **DNS name của ALB** qua cổng `80`. ALB chuyển yêu cầu đến một trong hai EC2 trong target group trên cổng `80`. Tại EC2, Nginx chuyển tiếp yêu cầu đến backend Node.js chạy ở `127.0.0.1:8080` bằng PM2.

```bash
Người dùng / Trình duyệt
        │ Gửi yêu cầu HTTP đến DNS của ALB
        ▼
Application Load Balancer — Listener HTTP:80
        │
        │ Kiểm tra các target đang Healthy
        │ Phân phối mỗi request đến một trong hai EC2
        │
        ├───────────────────────────────┐
        ▼                               ▼
EC2 Server 1                       EC2 Server 2
Nginx:80                           Nginx:80
        │                               │
        │ Reverse proxy                 │ Reverse proxy
        ▼                               ▼
Node.js:8080                      Node.js:8080
        │                               │
        └───────────┬───────────────────┘
                    ▼
              MongoDB Atlas
                    │
                    ▼
      Phản hồi → EC2 được chọn → ALB
                    │
                    ▼
               Người dùng
```
ALB sử dụng **health check** để xác định EC2 có thể nhận yêu cầu. Để tiếp tục phục vụ khi một EC2 gặp lỗi, target group cần có ít nhất **hai EC2 chạy cùng ứng dụng**, trong đó còn một EC2 ở trạng thái Healthy.

## Nội dung thực hiện

1. [Tạo target group](5.4.1-create_target_group/)
2. [Tạo Application Load Balancer](5.4.2-create_application_load_balancer/)
3. [Kiểm thử ALB](5.4.3-checkalb/)
4. [Tạo máy chủ EC2 thứ hai](5.4.4-create_second_ec2/)
5. [Đăng ký máy chủ EC2 thứ hai vào target group](5.4.5-register_second_ec2/)
