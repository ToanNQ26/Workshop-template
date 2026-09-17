---
title: "Tạo máy chủ EC2 thứ hai"
date: "2026-09-14"
weight: 4
chapter: false
pre: "<b> 5.4.4 </b>"
---

## Tổng quan
Trong bước này chúng ta sẽ nhân bản máy chủ ec2 backend trước đó để tăng khả năng chịu tải và lỗi của mô hình

---

## Các bước thực hiện

### Bước 1: Tạo AMI từ máy chủ EC2 trước đó
- Truy cập vào EC2, chọn instance
- Chọn Action -> Image and templates -> Create image
![Tạo AMI](/images/myimage/5_4/5_4_4/image1.png)
- Điền tên image, các mục còn lại để mặc định
![Tạo AMI](/images/myimage/5_4/5_4_4/image2.png)
- Kéo xuống và nhấn Create Image
![Tạo AMI](/images/myimage/5_4/5_4_4/image3.png)
### Bước 2: Tạo máy chủ nhân bản EC2 từ AMI
- Vẫn trong Ec2, kéo xuống và tìm mục Images, chọn AMIs
![Chọn AMI](/images/myimage/5_4/5_4_4/image4.png)
- Chọn AMI mà bạn vừa tạo -> Launch instance from AMI
![Chọn AMI](/images/myimage/5_4/5_4_4/image5.png)
- Ở bước cấu hình, làm theo các chỉ dẫn đã ghi ở 5.2.1
![Cấu hình EC2](/images/myimage/5_4/5_4_4/image6.png)
> **Lưu ý:** Ở phần network settings có thể cấu hình như này để dễ thao tác nhất, Cùng vpc với ec2 trước đó nhưng khác subnet

![Networksetting](/images/myimage/5_4/5_4_4/image7.png)
- Cuối cùng chọn Launch Instance ở bên phải
