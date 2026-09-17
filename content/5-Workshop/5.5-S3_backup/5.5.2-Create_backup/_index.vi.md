---
title: "Tạo backup database"
date: "2026-09-14"
weight: 2
chapter: false
pre: "<b> 5.5.2 </b>"
---

## Tổng quan

Trong bước này, chúng ta sử dụng **MongoDB Compass** để xuất toàn bộ dữ liệu của từng **collection** trong cơ sở dữ liệu ứng dụng và lưu thành các tệp trên máy tính. Thao tác được thực hiện lần lượt với các collection cần sao lưu để chuẩn bị bộ tệp dữ liệu tải lên Amazon S3.

Phạm vi thực hành tập trung vào **sao lưu dữ liệu bằng chức năng Export Data** của MongoDB Compass. Các tệp xuất ra là đầu vào cho bước lưu trữ bản sao lưu trên S3 ở phần tiếp theo.

---

## Các bước thực hiện:

### Bước 1: Sử dụng MongoDB Compass truy cập tới database
- Mở MongoDB Compass, kết nối tới database
![Kết nối dtb bằng mongodb compass](/images/myimage/5_5/5_5_2/image1.png)
- Click chuột vào collection muốn tạo backup, chọn export data -> export the full collection
![Tạo backup cho collection](/images/myimage/5_5/5_5_2/image2.png)
- Thực hiện lặp đi lặp lại cho đến khi tạo xong hết data backup cho các collection