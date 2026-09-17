---
title: "Kết nối SSH đến EC2"
date: "2026-07-10"
weight: 3
chapter: false
pre: "<b> 5.2.3 </b>"
---

## Tổng quan

SSH (Secure Shell) cung cấp kết nối mã hóa để quản trị EC2 từ máy tính cá nhân. Sử dụng OpenSSH và private key đã tải ở mục 5.2.1.

## Các bước thực hiện

### Bước 1: Kiểm tra điều kiện kết nối

Instance phải ở trạng thái **Running**, các status checks thành công và có public IPv4 address. Security group cho phép TCP port **22** từ **My IP**. Subnet cần route `0.0.0.0/0` đến Internet Gateway.

Trong EC2 Console, chọn instance và sao chép **Public IPv4 address**. Thay `PUBLIC_IP` trong các lệnh bằng địa chỉ này.

![Sao chép ipv4](/images/myimage/5_2_3/image1.png)

### Bước 2: Chuẩn bị SSH client

Trên máy tính cá nhân, mở PowerShell hoặc Terminal và chạy `ssh -V`. Nếu Windows chưa có SSH, cài **OpenSSH Client** trong Optional features.

Lưu `WebServer-Key.pem` trong thư mục riêng. Trên Windows, giới hạn quyền đọc cho tài khoản của bạn qua **Properties → Security → Advanced**. Trên Linux/macOS, chạy tại thư mục chứa key:

```bash
chmod 400 WebServer-Key.pem
```

### Bước 3: Kết nối đến máy chủ

Chạy trên máy tính cá nhân, tại thư mục chứa key:

```bash
ssh -i "WebServer-Key.pem" ec2-user@PUBLIC_IP
```

`ec2-user` là username mặc định của Amazon Linux 2023. Lần kết nối đầu tiên, xác minh host key fingerprint của instance trước khi nhập `yes`.

![Connect ssh](/images/myimage/5_2_3/image2.png)

### Bước 4: Xác nhận phiên SSH

Các lệnh sau được chạy **trên EC2**:

```bash
whoami
cat /etc/os-release
pwd
```

Xác nhận username là `ec2-user` và hệ điều hành là Amazon Linux 2023. Dùng `exit` để đóng phiên SSH.

## Xử lý lỗi

| Lỗi | Cách kiểm tra |
| --- | --- |
| Connection timed out | Public IP, rule SSH, route và network ACL. |
| Permission denied (publickey) | Username và private key phải khớp key pair của instance. |
| Unprotected private key file | Thu hẹp quyền truy cập private key. |
| Host key verification failed | Xác minh instance và fingerprint trước khi cập nhật host đã lưu. |

## Kết quả

Đã thiết lập phiên SSH và có thể cấu hình máy chủ.

## Tài liệu tham khảo

[AWS: Kết nối Linux instance bằng SSH](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/connect-to-linux-instance.html)
