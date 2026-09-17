---
title: "Tải bản backup lên S3"
date: "2026-09-14"
weight: 3
chapter: false
pre: "<b> 5.5.3 </b>"
---

## Tổng quan

Trong bước này, chúng ta tải các tệp dữ liệu đã xuất từ **MongoDB Compass** lên **S3 bucket** được tạo trước đó. Thao tác này đưa bản sao lưu từ máy tính lên nơi lưu trữ tập trung trên Amazon S3, giúp thuận tiện truy cập và tải về khi cần sử dụng.

Sau khi hoàn tất, các tệp sao lưu sẽ được lưu dưới dạng **object** trong bucket, khép lại quy trình tạo và lưu trữ bản sao lưu dữ liệu của workshop.

---

## Các bước thực hiện

### Bước 1: Truy cập S3 và chọn vào bucket đã tạo
- Chọn bucket đã tạo
![Chọn bucket](/images/myimage/5_5/5_5_3/image1.png)

### Bước 2: Tải bản backup lên S3
- Chọn vào upload ở giữa như hình bên dưới
![Upload](/images/myimage/5_5/5_5_3/image2.png)
- Kéo folder bạn đã lưu các bản backup trước đó vào giao diện S3
![Tải bản backup lên](/images/myimage/5_5/5_5_3/image3.png)
- Cuối cùng nhấn upload 
![Upload](/images/myimage/5_5/5_5_3/image4.png)