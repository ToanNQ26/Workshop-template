---
title: "Tạo target group"
date: "2026-09-14"
weight: 1
chapter: false
pre: "<b> 5.4.1 </b>"
---

## Tổng quan

Trong bước này chúng ta sẽ thực hiện tạo target group để chuẩn bị cho việc tạo Application Load Banlancer

---

## Các bước thực hiện

### Bước 1: Truy cập tới phần target group trong EC2:
Chúng ta cần truy cập vào EC2, sau đó cuộn chuột xuống và tìm tới phần Load Blancing,chọn target group
![Truy cập tới targer group](/images/myimage/5_4/5_4_1/image1.png)

### Bước 2: Cấu hình cơ bản cho target group
Ở trang hiện tại (sau bước 1), ấn vào phần Create target group:
- Chọn instances ( mặc định), viết tên group mà bạn định đặt.
![Tạo target group](/images/myimage/5_4/5_4_1/image2.png)
- Cấu hình protocol, Port, Ip addresstype,VPC,Protocol version như hình:
![Tạo target group](/images/myimage/5_4/5_4_1/image3.png)
> **Lưu ý:** VPC phải cùng mạng với máy chủ EC2 mà bạn chọn làm máy chủ backend trước đó
- Chọn heal check path, chọn bất kì 1 api trong project của bạn. vd: /home ( nếu bạn sử dụng project của tôi để làm theo thì có thể cấu hình như hình bên dưới):
![Tạo target group](/images/myimage/5_4/5_4_1/image4.png)
- Sau khi làm xong, ấn next để chuyển sang bước 3
### Bước 3: Chọn instance EC2 cho target group
- Tick vào instance EC2 mà bạn cấu hình cho backend trước đó, bạn cũng có thể về lại mục instance của EC2 để xem lại:
![Tạo target group](/images/myimage/5_4/5_4_1/image5.png)
- Nhập port cho instance để lắng nghe, sau đó ấn Include as pending below, kết quả sẽ như hình bên dưới:
![Tạo target group](/images/myimage/5_4/5_4_1/image6.png)
- Ấn next để sang bước tiếp theo
### Bước 4: Xem lại và tạo target group
- Bạn cần kiểm tra lại xem có đúng với cấu hình mà bạn đã chọn trước đó hay không, sau đó chỉ cần ấn Create target group
![Tạo target group](/images/myimage/5_4/5_4_1/image7.png)