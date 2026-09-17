---
title: "Tích hợp S3"
date: "2026-09-14"
weight: 5
chapter: false
pre: "<b> 5.5 </b>"
---

## Tổng quan

Trong phần này, chúng ta sử dụng **Amazon S3** làm nơi lưu trữ tập trung các tệp sao lưu dữ liệu của ứng dụng. Việc lưu một bản sao dữ liệu tách biệt với cơ sở dữ liệu đang hoạt động giúp chuẩn bị nguồn dữ liệu để phục hồi khi cần.

Quy trình thực hành gồm ba bước: tạo **S3 bucket**, dùng **MongoDB Compass** để xuất dữ liệu từ các collection, sau đó tải các tệp đã xuất lên S3. Qua đó, chúng ta hoàn thiện quy trình sao lưu dữ liệu thủ công cho mô hình triển khai của workshop.

---

## Kiến trúc triển khai

Kiến trúc sao lưu gồm ba thành phần chính: **cơ sở dữ liệu MongoDB**, **máy tính sử dụng MongoDB Compass** và **Amazon S3**. Dữ liệu được xuất từ MongoDB về máy tính, sau đó tải lên S3 để lưu trữ tách biệt với cơ sở dữ liệu đang phục vụ ứng dụng.


Luồng dữ liệu trong quá trình sao lưu:

```text
Cơ sở dữ liệu MongoDB
        │ Đọc dữ liệu từ từng collection
        ▼
MongoDB Compass trên máy tính
        │ Export Data — xuất toàn bộ dữ liệu của collection
        ▼
Các tệp dữ liệu lưu trên máy tính
        │ Tải lên qua AWS Management Console
        ▼
Amazon S3 bucket
        └ Lưu trữ các tệp sao lưu dưới dạng object
```

Trong phạm vi workshop, quy trình được **thực hiện thủ công**: người thực hiện lần lượt xuất dữ liệu của các collection cần sao lưu, sau đó tải bộ tệp lên bucket đã tạo. Khi cần sử dụng dữ liệu đã lưu, các tệp có thể được tải từ S3 về máy tính để phục vụ quá trình nhập lại dữ liệu vào MongoDB.

## Nội dung thực hiện

1. [Tạo S3 bucket để lưu trữ bản sao lưu](5.5.1-create_s3/)
2. [Tạo bản sao lưu dữ liệu bằng MongoDB Compass](5.5.2-create_backup/)
3. [Tải các tệp sao lưu lên Amazon S3](5.5.3-upload_to_s3/)
