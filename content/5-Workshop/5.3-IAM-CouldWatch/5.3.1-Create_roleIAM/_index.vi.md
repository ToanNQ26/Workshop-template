
---
title: "Tạo IAM role"
date: "2026-09-10"
weight: 1
chapter: false
pre: "<b> 5.3.1 </b>"
---

## Tổng quan

Trong bước này, chúng ta sẽ tiến hành tạo một IAM role cho EC2 để giúp EC2 có quyền gửi log tới CloudWatch

---
## Các bước thực hiện

### Bước 1: Truy cập dịch vụ IAM

Trên trang chủ quản lý tài khoản amazon của bạn, làm theo các bước sau:
- Nhập "IAM" vào thanh tìm kiếm ở phía trên bên trái
![Truy cập dịch vụ IAM](/images/myimage/5_3/5_3_1/image1.png)

- Click chuột vào IAM, sau đó chọn role

![Tạo role](/images/myimage/5_3/5_3_1/image2.png)

### Bước 2: Tạo role cho ec2

Từ trang hiện tại, ấn Create role phía trên góc phải màn hình:

- Chọn entity và usecase sau đó bấm next:
![Tạo role](/images/myimage/5_3/5_3_1/image3.png)

- Chọn chính sách quyền hạn, sau đó bấm next:
![Tạo role](/images/myimage/5_3/5_3_1/image4.png)

- Đặt tên, viết các cấu hình, kéo xuống dưới và bấm Create role
![Tạo role](/images/myimage/5_3/5_3_1/image5.png)