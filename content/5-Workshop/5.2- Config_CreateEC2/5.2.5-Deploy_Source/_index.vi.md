---
title: "Triển khai mã nguồn lên EC2"
date: "2026-07-10"
weight: 5
chapter: false
pre: "<b> 5.2.5 </b>"
---

## Tổng quan

Đưa mã nguồn lên EC2, cài dependencies.
## Các bước thực hiện

### Bước 1: Clone repository

Trên EC2, thay `YOUR_ACCOUNT` và `YOUR_REPOSITORY` bằng thông tin repository:

```bash
git clone https://github.com/YOUR_ACCOUNT/YOUR_REPOSITORY comic-website
cd comic-website
```

![Clone mã nguồn](/images/myimage/5_2_5/image1.png)

> **Lưu ý:** Nếu chưa có project cá nhân, bạn có thể sử dụng [Project Website Truyện Tranh](https://github.com/ToanNQ26/AppTruyen_Be) của tôi để thực hành triển khai lên EC2.

### Bước 2: Cài dependencies

```bash
npm install
```

Lệnh npm install giúp tải các thư viện cần thiết cho project sau khi clone từ github repo về.

![Cài dependencies](/images/myimage/5_2_5/image2.png)

### Bước 3: Cấu hình backend

Tạo `.env` trong thư mục backend bằng trình soạn thảo. Dùng `.env.example` của project làm mẫu; các biến sau chỉ là ví dụ:

```env
cd comic-website
nano .env
```

Backend phải đọc các biến này và nạp `.env`, chẳng hạn qua `dotenv`. Nếu bạn sử dụng project của tôi thì có thể cấu hình như này và thay vào các biến mà bạn tự tạo, bạn cũng có thể đọc qua readme.md để hiểu rõ hơn về project

![Cấu hình file env](/images/myimage/5_2_5/image3.png)

Sau đó nhấn Ctrl + O + Enter để lưu và Ctrl + X để thoát

## Kết quả

Mã nguồn, dependencies, cấu hình backend  đã sẵn sàng cho Nginx và PM2.

## Tài liệu tham khảo

[MongoDB Atlas: IP Access List](https://www.mongodb.com/docs/atlas/security/ip-access-list/)
