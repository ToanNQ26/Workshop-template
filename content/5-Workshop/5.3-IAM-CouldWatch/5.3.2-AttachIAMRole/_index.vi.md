---
title: "Gắn IAM role vào EC2"
date: "2026-09-10"
weight: 2
chapter: false
pre: "<b> 5.3.2 </b>"
---

## Tổng quan

Trong bước này chúng ta sẽ đi cấu hình cho máy chủ ec2 gửi log ra cloudwatch và gắn role đã tạo trước đó cho ec2 nhằm cấp quyền cho máy chủ gửi log

---

## Các bước thực hiện

### Bước 1: Truy cập vào ec2 instance

Chúng ta truy cập vào ec2 instance (nếu bạn quên cách truy cập có thể xem lại ở các bước 5.2), sau khi truy cập vào ec2 instance:
- Ở góc phải phía bên trên của instance, chọn Action-> Security -> Modify IAM role
![Gắn role cho ec2](/images/myimage/5_3/5_3_2/image1.png)
- Tiếp theo trong Modify IAM role,chọn mục IAM role chọn role đã tạo trước đó:
![Gắn role cho ec2](/images/myimage/5_3/5_3_2/image2.png)
Cuối cùng nhấn Update IAM role 