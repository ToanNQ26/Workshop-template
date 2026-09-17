---
title: "Tạo application load balancer"
date: "2026-09-14"
weight: 2
chapter: false
pre: "<b> 5.4.2 </b>"
---

## Tổng quan

Trong bước này, chúng ta sẽ tạo và cấu hình Application Load Balancer (ALB) để tiếp nhận và phân phối lưu lượng truy cập đến hai máy chủ Amazon EC2, giúp hệ thống hoạt động ổn định và tăng khả năng sẵn sàng.

---

## Các bước thực hiện

### Bước 1: Truy cập tới application load balancer:

Để truy cập tới application load balancer, chúng ta truy cập vào EC2, sau đó kéo xuống tìm phần Load Balancing
- Chọn Create load balancer:
![Truy cập application load balancer](/images/myimage/5_4/5_4_2/image1.png)

### Bước 2: Chọn Loadbalancer type:
- Ở trong bài thực hành này chúng ta chọn application load blancer
![Chọn application load balancer](/images/myimage/5_4/5_4_2/image2.png)

### Bước 3: Cấu hình cho ALB
- Điền tên theo ý của bạn và chọn các cấu hình như ảnh
![Cấu hình cho alb](/images/myimage/5_4/5_4_2/image3.png)
- Phần Network mapping, chọn cả 3 vùng mạng con theo VPC cùng với EC2 bạn tạo cho backend
![Network mapping](/images/myimage/5_4/5_4_2/image4.png)
- Phần Security groups, ngoài cấu hình mặc định bạn cần chọn thêm security group đang dùng cho máy backend EC2 cấu hình từ trước đó
![Security group](/images/myimage/5_4/5_4_2/image5.png)
- Phần Listeners and routing, chọn target group bạn vừa tạo từ bước 5.4.1 trước đó, còn lại để mặc định
![Listeners and routing](/images/myimage/5_4/5_4_2/image6.png)
- Cuối cùng ấn Create load balancer
![Create load balancer](/images/myimage/5_4/5_4_2/image7.png)
