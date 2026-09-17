---
title: "Cài đặt môi trường máy chủ"
date: "2026-07-10"
weight: 4
chapter: false
pre: "<b> 5.2.4 </b>"
---

## Tổng quan

Cài Git, Node.js, npm và PM2 trên Amazon Linux 2023. Chạy các lệnh trong bài **trên EC2 qua SSH**.

## Các bước thực hiện

### Bước 1: Cập nhật hệ thống và cài Git

```bash
sudo dnf upgrade -y
sudo dnf install -y git
git --version
```

Nếu cập nhật yêu cầu reboot, chạy `sudo reboot`, chờ instance sẵn sàng và kết nối lại.

### Bước 2: Cài Node.js và npm

Ví dụ dùng Node.js 24. Kiểm tra `engines` trong `package.json` và tài liệu project để chọn phiên bản tương thích.

```bash
sudo dnf install -y nodejs24 nodejs24-npm
node -v
npm -v
```

Nếu đã cài nhiều phiên bản, dùng `sudo alternatives --config node` để chọn phiên bản mặc định và kiểm tra lại. Không cần cài MongoDB Server trên EC2 vì project sử dụng MongoDB Atlas.

### Bước 3: Cài PM2

Cài PM2 toàn cục để sử dụng lệnh `pm2` trên máy chủ:

```bash
sudo npm install -g pm2
pm2 -v
```

`-g` cài đặt toàn cục; `sudo` cấp quyền ghi vào thư mục cài đặt hệ thống. Sau khi cài, chạy các lệnh quản lý ứng dụng bằng `ec2-user`, như hướng dẫn ở [mục 5.2.7 – Khởi chạy và quản lý ứng dụng](../5.2.7-run_application/).

 Sau khi làm xong tất cả có thể sử dụng các lệnh kiểm tra như :
```bash
node -v
pm2 -v
git -v
```

## Kết quả

Git, Node.js, npm và PM2 đã sẵn sàng.

## Tài liệu tham khảo

[AWS: Node.js trên Amazon Linux 2023](https://docs.aws.amazon.com/linux/al2023/ug/nodejs.html)


