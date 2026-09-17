---
title: "Install and Configure Nginx"
date: "2026-07-10"
weight: 6
chapter: false
pre: "<b> 5.2.6 </b>"
---

## Overview

Nginx acts as a reverse proxy for the backend running on EC2.

## Procedure

### Step 1: Install Nginx

Run on EC2:

```bash
sudo dnf install -y nginx
sudo systemctl enable --now nginx
```

![Install and start Nginx](/images/myimage/5_2_6/image1.png)

### Step 2: Configure the Website

Use `nano /etc/nginx/conf.d/comic-website.conf` with `sudo` privileges to open the configuration file, then add:

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

Press `Ctrl+O`, then `Enter` to save, and `Ctrl+X` to exit. Display the file with `cat` to verify that its contents match the example below.

![Nginx configuration](/images/myimage/5_2_6/image2.png)

### Step 3: Validate and Reload the Configuration

Use the following commands to validate and reload the configuration:

```bash
sudo nginx -t
sudo systemctl reload nginx
```

Once successful, use Postman or Chrome to verify access with a GET request. Replace `publicipv4` with the instance's public IPv4 address:

- **Postman:** `GET http://publicipv4/stoies?page=1`
- **Chrome:** `http://publicipv4/stoies?page=1`

![Verify access](/images/myimage/5_2_6/image3.png)

## Expected Outcomes

The backend is accessible through Nginx.

## References

[Nginx: proxy_pass](https://nginx.org/en/docs/http/ngx_http_proxy_module.html#proxy_pass), [Nginx: try_files](https://nginx.org/en/docs/http/ngx_http_core_module.html#try_files)
