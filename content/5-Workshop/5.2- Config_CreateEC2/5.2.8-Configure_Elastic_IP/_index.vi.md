---
title: "Cấu hình Elastic IP"
date: "2026-07-10"
weight: 8
chapter: false
pre: "<b> 5.2.8 </b>"
---

## Tổng quan

Elastic IP là public IPv4 tĩnh được cấp cho tài khoản AWS. Gán địa chỉ này cho EC2 để website giữ địa chỉ truy cập sau khi stop/start instance.

## Các bước thực hiện

### Bước 1: Allocate Elastic IP

Trong EC2 Console, chọn đúng Region của instance:

1. Chọn **Network & Security → Elastic IPs**.
![Vào elastic](/images/myimage/5_2_8/image1.png)
2. Chọn **Allocate Elastic IP address**.
![Vào elastic](/images/myimage/5_2_8/image1.png)
3. Để cấu hình mặc định như hình.
![Vào elastic](/images/myimage/5_2_8/image2.png)
4. Chọn **Allocate**;
![Vào elastic](/images/myimage/5_2_8/image2.png)

### Bước 2: Associate với EC2

1. Chọn Elastic IP vừa cấp.
![Chọn elastic](/images/myimage/5_2_8/image3.png)
2. Chọn **Actions → Associate Elastic IP address**.
3. Chọn **Resource type: Instance**.
4. Chọn `WebServer` và private IP của primary network interface.
5. Chọn **Associate**.
![Chọn instance ec2 cho elastic](/images/myimage/5_2_8/image4.png)

Public IPv4 tự động trước đó sẽ được thay thế. Phiên SSH dùng IP cũ có thể bị ngắt; kết nối lại bằng IP mới.


### Bước 3: Kiểm tra truy cập

Mở `http://ELASTIC_IP/` và kiểm tra API. Elastic IP không tự cấu hình HTTPS hay thay đổi security group.

![Kiểm tra](/images/myimage/5_2_8/image5.png)

## Chi phí và quản lý tài nguyên

AWS tính phí public IPv4, bao gồm Elastic IP đang gán hoặc chưa gán. **Disassociate** không đồng nghĩa với **Release**. Khi kết thúc workshop, chỉ release sau khi website và DNS không còn phụ thuộc địa chỉ này.

## Kết quả

EC2 có public IPv4 cố định.

## Tài liệu tham khảo

[AWS: Elastic IP addresses](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/elastic-ip-addresses-eip.html)
