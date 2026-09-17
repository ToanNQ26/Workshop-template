---
title: "Khởi chạy và quản lý ứng dụng"
date: "2026-07-10"
weight: 7
chapter: false
pre: "<b> 5.2.7 </b>"
---

## Tổng quan

PM2 duy trì backend sau khi đóng SSH và tự khởi chạy sau reboot. Chạy các lệnh PM2 bằng **ec2-user**, trừ lệnh thiết lập startup có `sudo` do PM2 cung cấp.

## Các bước thực hiện

### Bước 1: Khởi chạy bằng PM2

```bash
cd comic-website
sudo -i
pm2 start ./src/server.js --name webtruyen_be
```

Tiến trình cần ở trạng thái **online**, log không có lỗi khởi động hoặc database.

![Kiểm tra](/images/myimage/5_2_7/image1.png)

.

### Bước 2: Thiết lập tự khởi chạy

```bash
pm2 startup
```

Chạy **đúng lệnh có sudo mà PM2 in ra**, sau đó:

```bash
pm2 save
```

Startup script phụ thuộc user và đường dẫn Node.js. Tạo lại script nếu thay đổi phiên bản hoặc cách cài Node.js.

### Bước 3: Kiểm ta tiến trình ec2

Sử dụng lệnh như bên dưới để kiểm tra:

```bash
pm2 status
```
Nếu thành công sẽ có kết quả như hình

![Kiểm tra](/images/myimage/5_2_7/image2.png)


## Kết quả

Backend chạy dưới PM2, Nginx chuyển tiếp request API và danh sách tiến trình đã được lưu.

## Tài liệu tham khảo

[PM2: Quick Start](https://pm2.keymetrics.io/docs/usage/quick-start/), [PM2: Startup Script](https://pm2.keymetrics.io/docs/usage/startup/)
