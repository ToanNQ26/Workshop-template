
---
title: "Khởi tạo EC2 Instance"
date: "2026-07-10"
weight: 1
chapter: false
pre: "<b> 5.2.1 </b>"
---

## Tổng quan

Trong bước này, chúng ta sẽ tiến hành khởi tạo một **Amazon EC2 Instance** để làm máy chủ triển khai Project Website.

Amazon EC2 (Elastic Compute Cloud) là dịch vụ cung cấp máy chủ ảo trên nền tảng AWS. Sau khi EC2 Instance được tạo thành công, chúng ta có thể kết nối đến máy chủ, cài đặt môi trường cần thiết và triển khai Source Code của Project.

---

## Các bước thực hiện

### Bước 1: Truy cập dịch vụ EC2

- Đăng nhập vào **AWS Management Console**.
- Tại thanh tìm kiếm, nhập `EC2`.
- Chọn dịch vụ **EC2** từ kết quả tìm kiếm.

![Truy cập dịch vụ EC2](/images/myimage/5_2/01-ec2-service.png)

---

### Bước 2: Khởi tạo EC2 Instance mới

Tại giao diện quản lý **Amazon EC2**:

- Chọn **Instances** ở thanh điều hướng bên trái.
- Chọn **Launch instances** để bắt đầu quá trình tạo máy chủ mới.

![Chọn Launch instances](/images/myimage/5_2/02-ec2-service.png)

---

### Bước 3: Đặt tên cho EC2 Instance

Tại phần **Name and tags**, nhập tên cho EC2 Instance.

Ví dụ:

`WebServer`

Tên Instance giúp chúng ta dễ dàng nhận biết và quản lý máy chủ, đặc biệt khi có nhiều EC2 Instance trong cùng một tài khoản AWS.

![Đặt tên EC2 Instance](/images/myimage/5_2/03-ec2-service.png)

---

### Bước 4: Chọn Amazon Machine Image (AMI)

Tại phần **Application and OS Images (Amazon Machine Image)**, lựa chọn hệ điều hành sử dụng cho máy chủ.

Trong Project này, chúng ta lựa chọn:

- **Amazon Linux**
- **Amazon Linux 2023 AMI**
- **Architecture:** 64-bit (x86)

Amazon Linux là hệ điều hành được AWS cung cấp và tối ưu để hoạt động trên môi trường AWS.

![Chọn Amazon Linux AMI](/images/myimage/5_2/04-ec2-service.png)

---

### Bước 5: Chọn Instance Type

Tại phần **Instance type**, lựa chọn cấu hình phần cứng cho máy chủ.

Trong Project này, lựa chọn:

`t3.micro`

Instance Type quyết định các tài nguyên được cung cấp cho máy chủ như CPU, RAM và khả năng xử lý.

Đối với Project Website phục vụ mục đích thực hành với lượng truy cập thấp, cấu hình này phù hợp để triển khai và thử nghiệm ứng dụng, đồng thời giúp hạn chế chi phí sử dụng AWS.

![Chọn Instance Type](/images/myimage/5_2/05-ec2-service.png)

---

### Bước 6: Tạo Key Pair

**Key Pair** được sử dụng để xác thực khi kết nối SSH từ máy tính cá nhân đến EC2 Instance.

Tại phần **Key pair (login)**:

- Chọn **Create new key pair**.

![Chọn Create new key pair](/images/myimage/5_2/06-ec2-service.png)

Tiếp theo, cấu hình Key Pair:

- **Key pair name:** `WebServer-Key`
- **Key pair type:** RSA
- **Private key file format:** `.pem`

Sau đó chọn **Create key pair**.

Sau khi tạo thành công, file `.pem` sẽ được tải xuống máy tính.

> **Lưu ý:** Cần lưu trữ file Private Key `.pem` cẩn thận. File này được sử dụng để xác thực khi kết nối SSH đến EC2 Instance. Không nên chia sẻ Private Key hoặc đưa file này lên GitHub/Public Repository.

---

### Bước 7: Cấu hình Network Settings

Tại phần **Network settings**, cấu hình các thiết lập mạng cơ bản cho EC2 Instance.

Có thể sử dụng:

- **VPC:** Default VPC.
- **Subnet:** No preference.
- **Auto-assign Public IP:** Enable.

![Cấu hình Network Settings](/images/myimage/5_2/07-ec2-service.png)

Việc bật **Auto-assign Public IP** giúp EC2 Instance nhận một địa chỉ Public IPv4 để có thể kết nối với máy chủ thông qua Internet.

Tại phần Firewall, chúng ta có thể tạo một **Security Group** mới.

Trong bước này chỉ cần cấu hình cơ bản để phục vụ quá trình khởi tạo Instance. Security Group sẽ được cấu hình chi tiết ở phần tiếp theo.

---

### Bước 8: Cấu hình Storage

Tại phần **Configure storage**, lựa chọn dung lượng ổ đĩa cho máy chủ.

Ví dụ:

- **Volumes:** 1
- **Size:** 8 GiB
- **Volume type:** gp3

![Cấu hình Storage](/images/myimage/5_2/08-ec2-service.png)

Dung lượng Storage có thể được điều chỉnh tùy thuộc vào yêu cầu của Project.

Đối với Project Website có quy mô nhỏ, dung lượng này có thể đáp ứng nhu cầu cài đặt môi trường, thư viện và lưu trữ Source Code.

---

### Bước 9: Kiểm tra cấu hình và tạo Instance

Tại phần **Summary**, kiểm tra lại các thông tin đã cấu hình:

![Kiểm tra cấu hình](/images/myimage/5_2/09-ec2-service.png)

- Name.
- Amazon Machine Image (AMI).
- Instance Type.
- Key Pair.
- Network Settings.
- Security Group.
- Storage.

Sau khi kiểm tra các thông tin, chọn:

**Launch instance**

để tiến hành khởi tạo EC2 Instance.

![Launch EC2 Instance](/images/myimage/5_2/10-ec2-service.png)

---

### Bước 10: Kiểm tra trạng thái EC2 Instance

Sau khi quá trình khởi tạo hoàn tất:

- Chọn menu bên trái và bấm vào mục instance.
- Tìm EC2 Instance vừa tạo.
- Kiểm tra trạng thái hoạt động của Instance.

![Danh sách EC2 Instances](/images/myimage/5_2/11-ec2-service.png)

Đợi đến khi EC2 Instance hiển thị:

- **Instance state:** Running.
- **Status check:** 3/3 checks passed.

Khi đó, EC2 Instance đã sẵn sàng để sử dụng.

---

### Bước 11: Kiểm tra thông tin EC2 Instance

Chọn EC2 Instance vừa tạo để xem các thông tin chi tiết.

Một số thông tin quan trọng bao gồm:

- **Instance ID:** ID định danh của EC2 Instance.
- **Instance state:** Trạng thái hoạt động của máy chủ.
- **Instance type:** Cấu hình của máy chủ.
- **Public IPv4 address:** Địa chỉ IP Public của máy chủ.
- **Private IPv4 address:** Địa chỉ IP sử dụng bên trong VPC.
- **Public IPv4 DNS:** DNS Public của EC2 Instance.
- **Availability Zone:** Availability Zone mà Instance đang hoạt động.

![Thông tin EC2 Instance](/images/myimage/5_2/12-ec2-service.png)

> **Lưu ý:** Public IPv4 Address được cấp tự động cho EC2 Instance có thể thay đổi khi thực hiện **Stop** và sau đó **Start** lại Instance. Trong các bước tiếp theo, chúng ta sẽ cấu hình **Elastic IP** để cung cấp một địa chỉ IPv4 Public cố định cho máy chủ.

---

## Kết quả

Sau khi hoàn thành các bước trên, chúng ta đã:

- Khởi tạo thành công một **Amazon EC2 Instance**.
- Sử dụng **Amazon Linux** làm hệ điều hành cho máy chủ.
- Tạo **Key Pair** phục vụ kết nối SSH.
- Cấu hình Network và Storage cơ bản.
- EC2 Instance đã chuyển sang trạng thái **Running**.
- Máy chủ đã sẵn sàng cho các bước cấu hình và triển khai Project tiếp theo.

Ở bước tiếp theo, chúng ta sẽ tiến hành cấu hình **Security Group** để kiểm soát các kết nối ra vào máy chủ EC2.



