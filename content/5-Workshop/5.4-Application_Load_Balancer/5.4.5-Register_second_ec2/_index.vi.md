---
title: "Đăng ký ALB cho máy chủ thứ 2"
date: "2026-09-14"
weight: 5
chapter: false
pre: "<b> 5.4.5 </b>"
---

## Tổng quan
Trong bước này chúng ta sẽ đăng ký máy chủ ec2 backend thứ hai vào Application Load Balancer  để tăng khả năng chịu tải và lỗi của mô hình

---

## Các bước thực hiện

### Bước 1: Truy cập vào mục regiter trong target group
- Truy cập đến target group như đã hướng dẫn ở 5.4.1, ấn vào target group đã tạo trước đó
![Truy cập target group](/images/myimage/5_4/5_4_5/image1.png)

### Bước 2: Thêm máy chủ EC2 thứ hai vào target group
- Click chuột vào Register target ở góc dưới bên phải
![Truy cập register](/images/myimage/5_4/5_4_5/image2.png)
- Chọn máy chủ EC2 thứ hai mà bạn vừa tạo, port 80, rồi ấn Include as pending below
![Chọn instance Ec2](/images/myimage/5_4/5_4_5/image3.png)
- Kéo xuống, kiểm tra lại và ấn Register pending targets
![Đăng ký vào target group](/images/myimage/5_4/5_4_5/image4.png)
- Sau khi làm xong các bước, cần hiện kết quả 2 healthy như hình
![Hoàn tất](/images/myimage/5_4/5_4_5/image5.png)