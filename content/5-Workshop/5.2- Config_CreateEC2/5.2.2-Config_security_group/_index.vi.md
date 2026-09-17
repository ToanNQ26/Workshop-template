
---
title: "Cấu hình Security Group"
date: "2026-07-10"
weight: 2
chapter: false
pre: "<b> 5.2.2 </b>"
---

## Tổng quan

Sau khi khởi tạo EC2 Instance, chúng ta cần cấu hình **Security Group** để kiểm soát các kết nối ra vào máy chủ.

Security Group hoạt động như một **Virtual Firewall** dành cho EC2 Instance. Thông qua Security Group, chúng ta có thể xác định loại lưu lượng nào được phép truy cập vào máy chủ và lưu lượng nào được phép đi ra ngoài.

Trong Project này, Security Group sẽ được cấu hình để phục vụ các nhu cầu chính sau:

- Cho phép kết nối **SSH** để quản trị EC2 Instance.
- Cho phép truy cập Website thông qua **HTTP**.
- Cho phép truy cập Website thông qua **HTTPS** khi cấu hình SSL/TLS.
- Kiểm soát phạm vi IP được phép truy cập vào từng Port.

---

## Các bước thực hiện

### Bước 1: Truy cập EC2 Instance

Tại **AWS Management Console**:

- Truy cập dịch vụ **EC2**.
- Chọn **Instances**.
- Chọn EC2 Instance đã tạo ở bước trước và kéo xuống dưới cho đến khi thấy các tab như ảnh.

![Chọn EC2 Instance](/images/myimage/5_2-2/image1.png)

---

### Bước 2: Kiểm tra Security Group hiện tại

Trong giao diện chi tiết của EC2 Instance:

- Chọn tab **Security**.
- Tìm mục **Security groups**.
- Chọn Security Group đang được gán cho EC2 Instance.

![Kiểm tra Security Group](/images/myimage/5_2-2/image2.png)

Security Group hiện tại chứa các Rule kiểm soát lưu lượng truy cập vào và đi ra khỏi EC2 Instance, chúng ta cần cấu hình cho nó giống như trong hình để đảm bảo mọi thứ hoạt động theo dự án hiện tại.

---

### Bước 3: Chỉnh sửa Inbound Rules

Sau khi chọn tab Security Group, tại giao diện chi tiết:

- Chọn vào tên security group, vd: như hình ở bước 2 là launch-wizard-4.
- Sau đó tiếp tục click vào security group id, như hình dưới là sg-0505ab841db0cbd9f.


Inbound Rules xác định những kết nối từ bên ngoài được phép truy cập vào EC2 Instance.

![Inbound Rules](/images/myimage/5_2-2/image3.png)

Để chỉnh sửa Inbound Rules, chọn:

- **Edit inbound rules**

![Edit Inbound Rules](/images/myimage/5_2-2/image4.png)


### Bước 4: Cấu hình SSH

Đầu tiên, cấu hình Rule cho phép kết nối SSH đến EC2 Instance.

- chọn Add rule

Thêm Rule với cấu hình:

| Type | Protocol | Port Range | Source |
| --- | --- | --- | --- |
| SSH | TCP | 22 | My IP |

![Cấu hình SSH Rule](/images/myimage/5_2-2/image5.png)

Port **22** được sử dụng cho giao thức SSH, giúp chúng ta có thể kết nối và quản trị EC2 Instance từ máy tính cá nhân.

Tại phần **Source**, nên lựa chọn:

`My IP`

AWS sẽ tự động lấy địa chỉ Public IP hiện tại của máy tính đang truy cập AWS Management Console.

> **Lưu ý:** Không nên cấu hình SSH với Source là `0.0.0.0/0` nếu không thực sự cần thiết, vì điều này cho phép mọi địa chỉ IP trên Internet thử kết nối đến Port 22 của máy chủ.

---

### Bước 5: Cấu hình HTTP

Để người dùng có thể truy cập Website thông qua trình duyệt, thêm Rule cho giao thức HTTP.

Cấu hình:

| Type | Protocol | Port Range | Source |
| --- | --- | --- | --- |
| HTTP | TCP | 80 | Anywhere IPv4 |

![Cấu hình HTTP Rule](/images/myimage/5_2-2/image6.png)

Port **80** là Port mặc định của giao thức HTTP.

Tại phần **Source**, lựa chọn:

`Anywhere IPv4`

Tương ứng với:

`0.0.0.0/0`

Điều này cho phép người dùng từ Internet truy cập Website đang chạy trên EC2 Instance.

---

### Bước 6: Cấu hình HTTPS

Nếu Website được cấu hình SSL/TLS, cần cho phép kết nối thông qua giao thức HTTPS.

Thêm Rule:

| Type | Protocol | Port Range | Source |
| --- | --- | --- | --- |
| HTTPS | TCP | 443 | Anywhere IPv4 |

![Cấu hình HTTPS Rule](/images/myimage/5_2-2/image7.png)

Port **443** là Port mặc định được sử dụng cho giao thức HTTPS.

HTTPS giúp mã hóa dữ liệu giữa trình duyệt của người dùng và máy chủ, từ đó tăng tính bảo mật cho Website.

> **Lưu ý:** Nếu Project chưa sử dụng HTTPS ở thời điểm hiện tại thì Rule này có thể được bổ sung sau khi tiến hành cấu hình Domain và SSL/TLS.

---

### Bước 7: Kiểm tra các Inbound Rules

Sau khi thêm các Rule cần thiết, Security Group có thể bao gồm:

| Type | Protocol | Port | Source | Mục đích |
| --- | --- | --- | --- | --- |
| SSH | TCP | 22 | My IP | Quản trị máy chủ |
| HTTP | TCP | 80 | 0.0.0.0/0 | Truy cập Website bằng HTTP |
| HTTPS | TCP | 443 | 0.0.0.0/0 | Truy cập Website bằng HTTPS |

![Danh sách Inbound Rules](/images/myimage/5_2-2/image8.png)

Sau khi kiểm tra cấu hình, chọn:

**Save rules**

để lưu các thay đổi.

---

## Cấu hình Outbound Rules

### Bước 8: Kiểm tra Outbound Rules

Để cấu hình cho Outbuond rules, bạn cần thực hiện các bước sau:

- Chọn tab: Outbound rules
- chọn Edit outbound rules

![Outbound Rules](/images/myimage/5_2-2/image9.png)

Outbound Rules kiểm soát các kết nối đi từ EC2 Instance ra bên ngoài.

Theo mặc định, Security Group thường có Rule:

| Type | Protocol | Port Range | Destination |
| --- | --- | --- | --- |
| All traffic | All | All | 0.0.0.0/0 |

Rule này cho phép EC2 Instance kết nối đến Internet.

Điều này cần thiết để máy chủ có thể thực hiện các thao tác như:

Trong phạm vi Project này, chúng ta có thể giữ nguyên Outbound Rule mặc định.

---

## Kiểm tra Security Group

### Bước 9: Kiểm tra Security Group sau khi cấu hình

Sau khi hoàn tất, quay lại EC2 Instance:

- Chọn EC2 Instance.
- Chọn tab **Security**.
- Kiểm tra Security Group vừa cấu hình.

![Kiểm tra Security Group hoàn tất](/images/myimage/5_2-2/image10.png)

Đảm bảo các Inbound Rules cần thiết đã được thêm thành công.

---

## Một số lưu ý về bảo mật

Security Group là một trong những thành phần quan trọng giúp bảo vệ EC2 Instance.

Khi cấu hình Security Group, cần lưu ý:

- Chỉ mở những Port thực sự cần thiết.
- Không nên mở Port SSH `22` cho toàn bộ Internet nếu không cần thiết.
- Nên giới hạn SSH theo địa chỉ IP của máy quản trị.
- Không nên mở trực tiếp Port Database ra Internet nếu Database không yêu cầu truy cập Public.
- Port `80` và `443` có thể mở cho toàn bộ Internet nếu EC2 được sử dụng làm Web Server.
- Thường xuyên kiểm tra và loại bỏ những Rule không còn sử dụng.

> **Lưu ý:** Việc giới hạn các Port và Source IP giúp giảm bề mặt tấn công của máy chủ và hạn chế các truy cập không mong muốn từ Internet.

---

## Kết quả

Sau khi hoàn thành bước này, chúng ta đã:

- Xác định Security Group đang được sử dụng bởi EC2 Instance.
- Cấu hình Port **22** cho kết nối SSH.
- Cấu hình Port **80** cho HTTP.
- Cấu hình Port **443** cho HTTPS.
- Kiểm tra Outbound Rules của máy chủ.
- Giới hạn kết nối SSH theo địa chỉ IP của máy quản trị.
- Hoàn tất lớp Firewall cơ bản cho EC2 Instance.

EC2 Instance hiện đã sẵn sàng để thực hiện kết nối SSH và tiếp tục cài đặt môi trường cho máy chủ.


