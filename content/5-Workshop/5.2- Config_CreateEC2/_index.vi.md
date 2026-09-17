
---
title: "Cấu hình và tạo máy chủ EC2"
date: "2026-07-10"
weight: 2
chapter: false
pre: "<b> 5.2 </b>"
---

## Tổng quan

Trong chương này, chúng ta sẽ thực hiện **khởi tạo và cấu hình máy chủ Amazon EC2** để triển khai Project Website lên môi trường AWS.

Amazon EC2 (Elastic Compute Cloud) là dịch vụ cung cấp máy chủ ảo trên nền tảng AWS. EC2 sẽ được sử dụng làm máy chủ chính để chạy ứng dụng và tiếp nhận các yêu cầu từ người dùng thông qua Internet.

Trong quá trình triển khai, chúng ta sẽ thực hiện các nội dung chính sau:

- Khởi tạo một **EC2 Instance**.
- Cấu hình **Security Group** để kiểm soát lưu lượng mạng ra vào máy chủ.
- Kết nối đến máy chủ EC2 thông qua **SSH**.
- Cài đặt các công cụ và môi trường cần thiết để chạy Project.
- Đưa Source Code của Project lên máy chủ EC2.
- Cài đặt và cấu hình **Nginx** làm Web Server/Reverse Proxy.
- Khởi chạy Project trên máy chủ EC2.
- Cấu hình **Elastic IP** để duy trì địa chỉ IPv4 Public cố định cho máy chủ.
- Kiểm tra khả năng truy cập Website từ Internet.

---

## Kiến trúc triển khai

Trong mô hình này, **Amazon EC2** đóng vai trò là máy chủ chạy ứng dụng. Người dùng có thể gửi request từ Internet đến máy chủ thông qua địa chỉ Public IP.

**Security Group** được sử dụng như một lớp tường lửa ảo để kiểm soát các kết nối được phép truy cập vào EC2, chẳng hạn như:

- **SSH (Port 22):** Sử dụng để quản trị máy chủ từ xa.
- **HTTP (Port 80):** Cho phép người dùng truy cập Website thông qua giao thức HTTP.
- **HTTPS (Port 443):** Sử dụng khi Website được cấu hình SSL/TLS.

Ngoài ra, chúng ta sẽ sử dụng **Elastic IP** để gán một địa chỉ IPv4 Public cố định cho EC2 Instance. Điều này giúp địa chỉ IP của máy chủ không bị thay đổi sau khi Instance được Stop và Start lại.

---

## Nội dung thực hiện

Quá trình cấu hình và triển khai máy chủ EC2 được chia thành các bước sau:

1. [Khởi tạo EC2 Instance](5.2.1-createec2/)
2. [Cấu hình Security Group](5.2.2-config_security_group/)
3. [Kết nối SSH đến EC2](5.2.3-connect_ssh/)
4. [Cài đặt môi trường cho máy chủ](5.2.4-setup_server/)
5. [Đưa Source Code lên EC2](5.2.5-deploy_source/)
6. [Cài đặt và cấu hình Nginx](5.2.6-configure_nginx/)
7. [Khởi chạy Project trên EC2](5.2.7-run_application/)
8. [Cấu hình Elastic IP](5.2.8-configure_elastic_ip/)

> **Lưu ý:** Tên và đường dẫn của các mục trên có thể được thay đổi tùy theo cấu trúc thư mục của Project báo cáo.


