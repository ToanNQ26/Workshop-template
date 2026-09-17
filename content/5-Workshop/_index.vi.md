---
title : "Workshop"
date : "`r Sys.Date()`"
weight : 5
chapter : false
pre : " <b> 5. </b> "
---

# Bản hướng dẫn chi tiết về việc xây dựng kiến trúc hạ tầng cho web truyện tranh

#### Tổng quan bài Thực hành (Workshop)

Nội dung phần Workshop được cấu trúc thành 5 chương chính từ 5.1 đến 5.5 và các bài thực hành chi tiết 5.x.y dưới đây:

> [!NOTE]
>
> * Link Web Demo: [Web Demo](https://webtruyenbyquoctoan.netlify.app/)
> * [Backend](https://github.com/ToanNQ26/AppTruyen_Be)
> * [Frontend](https://github.com/ToanNQ26/AppTruyen_Fe)
---

#### Danh sách các chương thực hành:

1. [5.1. Công tác chuẩn bị](5.1-prepare/)

2. [5.2. Khởi tạo và cấu hình máy chủ EC2](5.2-config_createec2/)
   * [5.2.1. Khởi tạo EC2 Instance](5.2-config_createec2/5.2.1-createec2/)
   * [5.2.2. Cấu hình Security Group](5.2-config_createec2/5.2.2-config_security_group/)
   * [5.2.3. Kết nối SSH đến EC2](5.2-config_createec2/5.2.3-connect_ssh/)
   * [5.2.4. Cài đặt môi trường máy chủ](5.2-config_createec2/5.2.4-setup_server/)
   * [5.2.5. Triển khai mã nguồn lên EC2](5.2-config_createec2/5.2.5-deploy_source/)
   * [5.2.6. Cài đặt và cấu hình Nginx](5.2-config_createec2/5.2.6-configure_nginx/)
   * [5.2.7. Khởi chạy và quản lý ứng dụng](5.2-config_createec2/5.2.7-run_application/)
   * [5.2.8. Cấu hình Elastic IP](5.2-config_createec2/5.2.8-configure_elastic_ip/)

3. [5.3. Cấu hình IAM và giám sát log PM2 với CloudWatch](5.3-iam-couldwatch/)
   * [5.3.1. Tạo IAM role](5.3-iam-couldwatch/5.3.1-create_roleiam/)
   * [5.3.2. Gắn IAM role cho EC2](5.3-iam-couldwatch/5.3.2-attachiamrole/)
   * [5.3.3. Cấu hình CloudWatch Agent cho EC2](5.3-iam-couldwatch/5.3.3-configurepm2logs/)

4. [5.4. Cấu hình Application Load Balancer](5.4-application_load_balancer/)
   * [5.4.1. Tạo target group](5.4-application_load_balancer/5.4.1-create_target_group/)
   * [5.4.2. Tạo Application Load Balancer](5.4-application_load_balancer/5.4.2-create_application_load_balancer/)
   * [5.4.3. Kiểm thử ALB](5.4-application_load_balancer/5.4.3-checkalb/)
   * [5.4.4. Tạo máy chủ EC2 thứ hai](5.4-application_load_balancer/5.4.4-create_second_ec2/)
   * [5.4.5. Đăng ký máy chủ EC2 thứ hai vào target group](5.4-application_load_balancer/5.4.5-register_second_ec2/)

5. [5.5. Tích hợp S3](5.5-s3_backup/)
   * [5.5.1. Tạo S3 bucket để lưu trữ bản sao lưu](5.5-s3_backup/5.5.1-create_s3/)
   * [5.5.2. Tạo bản sao lưu dữ liệu bằng MongoDB Compass](5.5-s3_backup/5.5.2-create_backup/)
   * [5.5.3. Tải các tệp sao lưu lên Amazon S3](5.5-s3_backup/5.5.3-upload_to_s3/)
