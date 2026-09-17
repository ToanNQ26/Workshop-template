---
title: "Cài đặt và cấu hình Nginx"
date: "2026-07-10"
weight: 6
chapter: false
pre: "<b> 5.2.6 </b>"
---

## Tổng quan

Nginx phục vụ backend chạy trên EC2.

## Các bước thực hiện

### Bước 1: Cài Nginx

Chạy trên EC2:

```bash
sudo dnf install -y nginx
sudo systemctl enable --now nginx
```
![Cài và bật nginx](/images/myimage/5_2_6/image1.png)


### Bước 2: Cấu hình website

Sư dụng lệnh  `nano /etc/nginx/conf.d/comic-website.conf` bằng trình soạn thảo với `sudo` và thêm cấu hình bên dưới.

```nginx
server {
    listen 80;
    server_name _;

    location / {
        proxy_pass http://127.0.0.1:8080;

        proxy_http_version 1.1;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
    }
}
```
Sau đó Ctrl + O + Enter để lưu và Ctrl + X để thoát. Kết quả sẽ như hình bên dưới nếu dùng lệnh cat để kiểm tra lại

![Cấu hình](/images/myimage/5_2_6/image2.png)

### Bước 3: Kiểm tra và nạp cấu hình

Sử dụng 2 lệnh bên dưới để nạp và kiểm tra cấu hình

```bash
sudo nginx -t
sudo systemctl reload nginx
```

Nếu thành công thì hãy sử dụng các công cụ như postman hoặc chrome để kiểm tra lại lần cuối với lệnh get.  
Vd:Postman: get http://publicipv4/stoies?page=1  
 Chrome: http://publicipv4/stoies?page=1

![Kiểm tra](/images/myimage/5_2_6/image3.png)


## Kết quả

Backend được phục vụ bởi Nginx.

## Tài liệu tham khảo

[Nginx: proxy_pass](https://nginx.org/en/docs/http/ngx_http_proxy_module.html#proxy_pass), [Nginx: try_files](https://nginx.org/en/docs/http/ngx_http_core_module.html#try_files)
