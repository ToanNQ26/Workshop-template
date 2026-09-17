---
title: "Cấu hình Cloudwatch agent cho EC2"
date: "2026-09-10"
weight: 3
chapter: false
pre: "<b> 5.3.3 </b>"
---

## Tổng quan

Trong bước này chúng ta sẽ cấu hình cho máy chủ ec2 gửi log pm2 đến CloudWatch

---

## Các bước thực hiện

### Bước 1: Kết nối tới máy chủ EC2 bằng ssh

Sử dụng ssh để kết nối tới máy chủ(nếu bạn quên cách kết nối có thể quay lại bước 5.2.3 để xem lại)
- Sau khi kết nối thành công, sử dụng lệnh dưới để lấy quyền root:
```bash
sudo -i
```
### Bước 2: Cấu hình gửi log cho EC2 

Làm theo các bước hướng dẫn bên dưới:
- Chạy lệnh `pm2 describe webtruyen_be` trong terminal đã kết nối với ec2 và ghi lại hai dòng out log path và error log path
![Cấu hình gửi log cho EC2](/images/myimage/5_3/5_3_3/image1.png)

- Chạy lệnh `sudo dnf install amazon-cloudwatch-agent -y` để cài đặt agent cho ec2(có thể bỏ sudo nếu bạn đã làm theo bước 1):
![Cấu hình gửi log cho EC2](/images/myimage/5_3/5_3_3/image2.png) 

-Chạy lệnh `sudo nano /opt/aws/amazon-cloudwatch-agent/etc/amazon-cloudwatch-agent.json` để tạo file cấu hình, sau đó dán đoạn bên dưới vào file rồi lưu:
```bash
{
  "logs": {
    "logs_collected": {
      "files": {
        "collect_list": [
          {
            "file_path": "/root/.pm2/logs/webtruyen-be-out.log",
            "log_group_name": "/webtruyen/backend",
            "log_stream_name": "{instance_id}/out"
          },
          {
            "file_path": "/root/.pm2/logs/webtruyen-be-error.log",
            "log_group_name": "/webtruyen/backend",
            "log_stream_name": "{instance_id}/error"
          }
        ]
      }
    }
  }
}
```
![Cấu hình gửi log cho EC2](/images/myimage/5_3/5_3_3/image3.png) 

- Chạy lệnh `sudo /opt/aws/amazon-cloudwatch-agent/bin/amazon-cloudwatch-agent-ctl -a fetch-config -m ec2 -s -c file:/opt/aws/amazon-cloudwatch-agent/etc/amazon-cloudwatch-agent.json` để khởi động
![Cấu hình gửi log cho EC2](/images/myimage/5_3/5_3_3/image4.png)

- Cuối cùng chạy `sudo /opt/aws/amazon-cloudwatch-agent/bin/amazon-cloudwatch-agent-ctl -a status -m ec2` để kiểm tra, nếu thấy running nghĩa là thành công
![Cấu hình gửi log cho EC2](/images/myimage/5_3/5_3_3/image5.png)

Từ giờ khi bạn muốn xem log, chỉ cần vào CloudWatch-> Log Management -> Chọn log group mà bạn vừa tạo -> Xem log

![Kết quả](/images/myimage/5_3/5_3_3/image6.png)