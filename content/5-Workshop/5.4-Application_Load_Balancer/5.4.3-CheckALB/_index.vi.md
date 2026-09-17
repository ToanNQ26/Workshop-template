---
title: "Kiểm thử ALB"
date: "2026-09-14"
weight: 3
chapter: false
pre: "<b> 5.4.3 </b>"
---

## Tổng quan
Ở phần này, chúng ta sẽ kiểm thử ALB xem nó có thật sự hoạt động chưa,chúng ta cần kiểm thử ngay trước khi tạo EC2 thứ hai để có thể quay lại khắc phục một cách đơn giản nhất, tránh cho việc sau khi tạo xong hết nhưng lại không chạy được alb

## Các bước thực hiện

### Bước 1: Lấy link dns của ALB
- Truy cập vào application load balancer
- Chọn load balancer mà bạn vừa tạo, như trong hình là webtruyentranh
![Chọn load balancer](/images/myimage/5_4/5_4_3/image1.png)
- Sao chép link dns của ALB
![Lấy link dns](/images/myimage/5_4/5_4_3/image2.png)

### Bước 2: Kiểm tra
- Sử dụng postman hoặc chrome để test api mà bạn đã đưa vào trong target group, vd: `http://webtruyentranh-306793996.ap-southeast-1.elb.amazonaws.com/stories` vì trước đó tôi đã điền api stories vào target group ở bước 5.4.1
![Api](/images/myimage/5_4/5_4_1/image4.png)
- Dán vào chrome nếu api trong mã nguồn yêu cầu phương thức Get, nếu không phải Get bạn nên sử dụng postman để kiểm tra
![Kiểm tra api healthy đã được đăng ký](/images/myimage/5_4/5_4_3/image3.png)
