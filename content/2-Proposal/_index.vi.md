---
title: "Bản đề xuất"
date: "2026-09-16"
weight: 2
chapter: false
pre: "<b> 2. </b>"
---

# Xây dựng hạ tầng AWS có khả năng cân bằng tải cho Web Truyện Tranh

## 1. Tổng quan dự án

Dự án **Web Truyện Tranh** là một hệ thống đọc truyện trực tuyến gồm Frontend được phát triển bằng React, Backend sử dụng Node.js/Express, cơ sở dữ liệu MongoDB Atlas và Cloudinary để lưu trữ, phân phối hình ảnh truyện.

Đề xuất này tập trung xây dựng hạ tầng cho Backend trên Amazon Web Services theo hướng nâng cao tính sẵn sàng, hỗ trợ phân phối tải, giám sát tập trung và bảo vệ dữ liệu sao lưu.

Backend Node.js/Express được triển khai trên **hai máy chủ Amazon EC2**. Trên mỗi máy chủ, ứng dụng được quản lý bằng **PM2** và chạy tại địa chỉ `127.0.0.1:8080`. **Nginx** tiếp nhận yêu cầu tại cổng 80 và chuyển tiếp đến ứng dụng Backend thông qua cơ chế reverse proxy.

**Application Load Balancer (ALB)** đóng vai trò là điểm truy cập chung của Backend, tiếp nhận yêu cầu từ người dùng và phân phối từng request đến một trong các EC2 đang hoạt động tốt trong **Target Group**. Target Group thực hiện health check định kỳ để ALB chỉ chuyển tiếp lưu lượng đến những máy chủ có trạng thái `Healthy`.

**Elastic IP** được gắn với máy chủ chính nhằm duy trì địa chỉ IP ổn định cho hoạt động quản trị và kiểm thử trực tiếp. **AWS IAM** được sử dụng để cấp quyền cho EC2 truy cập các dịch vụ AWS cần thiết mà không phải lưu Access Key trực tiếp trên máy chủ.

**Amazon CloudWatch** thu thập và tập trung log ứng dụng từ các EC2, hỗ trợ theo dõi hoạt động và phát hiện lỗi trong quá trình vận hành. **Amazon S3** được sử dụng để lưu trữ các bản sao dữ liệu MongoDB, tạo thêm một lớp bảo vệ dữ liệu độc lập với cơ sở dữ liệu đang hoạt động.

Frontend tiếp tục được triển khai trên Netlify, dữ liệu chính tiếp tục được lưu trên MongoDB Atlas và hình ảnh truyện tiếp tục được quản lý bằng Cloudinary. Phương án này giúp tận dụng các thành phần hiện có, tập trung cải thiện hạ tầng Backend và hạn chế rủi ro khi phải chuyển đổi toàn bộ hệ thống trong cùng một giai đoạn.

### Mục tiêu dự án

Mục tiêu của dự án là xây dựng hạ tầng Backend trên AWS có khả năng hoạt động ổn định, phân phối lưu lượng giữa nhiều máy chủ và duy trì dịch vụ khi một máy chủ gặp sự cố.

Các mục tiêu cụ thể bao gồm:

- Triển khai Backend Node.js/Express trên hai máy chủ Amazon EC2.
- Sử dụng Application Load Balancer để cung cấp một điểm truy cập chung và phân phối request giữa hai EC2.
- Sử dụng Target Group và health check để chỉ chuyển lưu lượng đến các máy chủ đang hoạt động tốt.
- Tập trung log ứng dụng trên Amazon CloudWatch để hỗ trợ giám sát và xử lý sự cố.
- Sử dụng IAM Role để cấp quyền truy cập dịch vụ cho EC2 mà không lưu Access Key trực tiếp trên máy chủ.
- Lưu trữ bản sao dữ liệu MongoDB trên Amazon S3 nhằm hỗ trợ khôi phục dữ liệu khi cần thiết.
- Giữ nguyên các thành phần đang hoạt động ổn định gồm Netlify, MongoDB Atlas và Cloudinary để giảm phạm vi chuyển đổi.
- Xây dựng nền tảng để có thể tiếp tục bổ sung HTTPS, Route 53 và Auto Scaling trong giai đoạn phát triển tiếp theo.

---

## 2. Tuyên bố vấn đề

### 2.1. Hiện trạng

Hệ thống đã có đầy đủ Frontend, Backend, cơ sở dữ liệu và dịch vụ lưu trữ hình ảnh. Tuy nhiên, mô hình Backend chỉ chạy trên một máy chủ tạo ra điểm lỗi đơn, chưa có cơ chế phân phối yêu cầu, log còn phân tán và bản sao dữ liệu chưa được quản lý trên một kho độc lập.

Hạ tầng cần giải quyết các yêu cầu sau:

- Duy trì Backend khi một máy chủ gặp sự cố.
- Phân phối lưu lượng giữa nhiều máy chủ.
- Giữ địa chỉ IP quản trị ổn định cho máy chủ chính.
- Chỉ chuyển request đến máy chủ còn hoạt động tốt.
- Quản lý quyền AWS an toàn theo nguyên tắc quyền tối thiểu.
- Thu thập log tập trung để kiểm tra lỗi.
- Lưu bản sao MongoDB ngoài hệ thống cơ sở dữ liệu đang vận hành.

### 2.2. Vấn đề, giải pháp và lợi ích

| Vấn đề cần giải quyết | Dịch vụ hoặc giải pháp | Lý do lựa chọn và lợi ích |
|---|---|---|
| Một Backend Server tạo điểm lỗi đơn và giới hạn năng lực xử lý | **Hai Amazon EC2** | EC2 cho phép chủ động cấu hình hệ điều hành, Node.js, PM2 và Nginx. Hai máy giúp duy trì phục vụ khi một máy lỗi và tạo nền tảng mở rộng ngang. |
| Public IPv4 có thể thay đổi sau khi dừng và khởi động EC2 | **Elastic IP** | Cung cấp địa chỉ IPv4 tĩnh cho máy chủ chính, giúp quản trị, SSH và kiểm thử trực tiếp ổn định. Elastic IP không thay thế địa chỉ truy cập công khai qua ALB. |
| Chưa có điểm tiếp nhận và phân phối lưu lượng chung | **Application Load Balancer** | ALB tiếp nhận HTTP tại cổng 80, phân phối request đến các EC2 còn khỏe và cung cấp một DNS name duy nhất. |
| Cần quản lý máy chủ đích và loại bỏ máy lỗi khỏi luồng truy cập | **Target Group** | Đăng ký hai EC2, thực hiện health check và chỉ cho ALB chuyển tiếp đến target có trạng thái `Healthy`. |
| Không nên lưu Access Key trực tiếp trên EC2 | **AWS IAM Role** | IAM Role cấp thông tin xác thực tạm thời, giới hạn quyền đúng nhu cầu và giảm rủi ro lộ khóa bí mật. |
| Log PM2 nằm riêng trên từng EC2 | **Amazon CloudWatch** | CloudWatch Agent gửi log output/error lên một Log Group chung, phân biệt bằng instance ID, giúp kiểm tra mà không cần SSH vào từng máy. |
| Cần bản sao độc lập với MongoDB Atlas | **Amazon S3** | S3 có độ bền cao, hỗ trợ mã hóa, versioning và lifecycle; phù hợp lưu JSON hoặc archive do `mongodump` tạo. |
| Backend Node.js không nên mở trực tiếp ra Internet | **Nginx và Security Group** | Nginx nhận request tại cổng 80 rồi chuyển đến `127.0.0.1:8080`; Security Group giới hạn nguồn truy cập và không công khai cổng 8080. |

### 2.3. Lợi ích tổng thể

- Giảm phụ thuộc vào một Backend Server duy nhất.
- Tự động phân phối request giữa các EC2 đang hoạt động tốt.
- Tập trung log và đơn giản hóa phát hiện sự cố.
- Không lưu thông tin xác thực dài hạn trên máy chủ.
- Có bản sao dữ liệu độc lập để hỗ trợ khôi phục.
- Giữ nguyên Netlify, Cloudinary và MongoDB Atlas, qua đó giảm phạm vi thay đổi.

---

## 3. Kiến trúc giải pháp

### 3.1. Sơ đồ kiến trúc tổng thể

![Sơ đồ kiến trúc](/images/myimage/sodo1.png)

### 3.2. Thành phần kiến trúc

| Thành phần | Cấu hình chính | Vai trò |
|---|---|---|
| Amazon EC2 | 2 instance Amazon Linux 2023 ở các Availability Zone khác nhau | Chạy Node.js/Express, PM2 và Nginx |
| Elastic IP | Gắn với EC2 chính | IP ổn định cho quản trị và kiểm thử trực tiếp |
| Application Load Balancer | Internet-facing, Listener HTTP:80 | Điểm truy cập chung và phân phối request |
| Target Group(Trong ALB) | Instances, HTTP:80, HTTP1 | Quản lý hai EC2 và health check |
| IAM Role | Gắn vào EC2, least privilege | Cấp quyền CloudWatch và S3 không cần Access Key cục bộ |
| Amazon CloudWatch | Log Group `/webtruyen/backend` | Lưu log output/error theo instance ID |
| Amazon S3 | Private bucket, Block Public Access | Lưu bản sao MongoDB và áp dụng lifecycle |
| MongoDB Atlas | Cơ sở dữ liệu dùng chung | Lưu dữ liệu nghiệp vụ chính |
| Netlify | Nền tảng Frontend hiện tại | Phân phối ứng dụng React, cung cấp proxy kết nối tới dns của alb |
| Cloudinary | Dịch vụ hình ảnh hiện tại | Lưu và phân phối ảnh truyện |

### 3.3. Luồng xử lý yêu cầu

1. Frontend gửi API request đến DNS name của ALB.
2. Listener HTTP:80 của ALB áp dụng quy tắc chuyển tiếp đến Target Group `webtruyentranh`.
3. Target Group lựa chọn một trong hai EC2 đang `Healthy`.
4. Nginx trên EC2 nhận request tại cổng 80 và reverse proxy đến Node.js tại `127.0.0.1:8080`.
5. Backend xử lý nghiệp vụ, truy vấn MongoDB Atlas hoặc sử dụng Cloudinary khi cần.
6. Phản hồi đi ngược qua Nginx và ALB để trả về người dùng.

### 3.4. Health check và xử lý lỗi

Target Group thực hiện health check HTTP đến endpoint `/stories` trên cổng 80. Khi endpoint trả mã thành công, target được đánh dấu `Healthy`.

Nếu một EC2 liên tục không vượt qua health check, ALB tạm ngừng gửi request đến máy đó và tiếp tục phục vụ qua target còn khỏe.

### 3.5. Luồng log và sao lưu

- CloudWatch Agent đọc log PM2 trên từng EC2 và gửi đến `/webtruyen/backend`.
- Log stream dùng instance ID và loại log (`out` hoặc `error`) để phân biệt nguồn.
- Dữ liệu MongoDB được xuất định kỳ dưới dạng JSON hoặc archive `mongodump`, sau đó tải lên S3.
- Bản sao cần được restore thử định kỳ. Việc tải lên S3 nhưng chưa thử khôi phục chưa đủ để xác nhận quy trình sao lưu hoạt động.

---

## 4. Triển khai kỹ thuật

### 4.1. EC2, PM2 và Nginx

- Khởi tạo EC2 Amazon Linux 2023 trong cùng VPC với ALB.
- Cài đặt Node.js, npm, PM2 và Nginx.
- Triển khai Backend và cấu hình biến môi trường.
- Chạy Node.js tại cổng 8080 bằng PM2.
- Cấu hình Nginx tại cổng 80 reverse proxy đến `http://127.0.0.1:8080`.
- Lưu cấu hình PM2 để ứng dụng tự khởi động cùng hệ điều hành.

### 4.2. Elastic IP và Security Group

- Cấp phát Elastic IP và gắn vào EC2 chính.
- Security Group của ALB cho phép HTTP:80 từ Internet.
- Security Group của EC2 cho phép HTTP:80 từ Security Group của ALB.
- SSH:22 chỉ cho phép từ địa chỉ IP quản trị cần thiết.
- Không mở cổng 8080 ra Internet.

### 4.3. Target Group và ALB

- Tạo Target Group loại `Instances`, giao thức `HTTP:80`, phiên bản `HTTP1`.
- Đặt Health check protocol là `HTTP`.
- Đặt Health check path là `/stories`.
- Tạo ALB loại `Internet-facing` trên ít nhất hai subnet thuộc hai Availability Zone.
- Tạo Listener `HTTP:80`.
- Đặt Default action chuyển tiếp đến Target Group `webtruyentranh`.
- Kiểm tra DNS name của ALB trả phản hồi thành công.

### 4.4. EC2 thứ hai

- Tạo AMI từ EC2 đã được cấu hình ổn định.
- Khởi tạo EC2 thứ hai từ AMI tại Availability Zone khác.
- Kiểm tra biến môi trường, PM2, Nginx và kết nối MongoDB Atlas.
- Đăng ký cả hai EC2 vào Target Group tại cổng 80.
- Chờ cả hai máy chuyển sang trạng thái `Healthy`.
- Không lưu session hoặc tệp nghiệp vụ chỉ trên ổ đĩa cục bộ nếu hai máy cần thay thế nhau.

### 4.5. IAM và CloudWatch

- Tạo IAM Role có Trusted entity là EC2.
- Gắn policy `CloudWatchAgentServerPolicy`.
- Nếu EC2 tải bản sao lên S3, thêm policy riêng chỉ cho phép các thao tác cần thiết trên đúng bucket và prefix.
- Gắn IAM Role vào cả hai EC2.
- Không tạo Access Key dài hạn trên máy chủ.
- Cài đặt CloudWatch Agent trên cả hai EC2.
- Khai báo đúng đường dẫn log PM2 thực tế.
- Đặt Log Group là `/webtruyen/backend`.
- Đặt Log Stream theo mẫu `{instance_id}/out` và `{instance_id}/error`.
- Nạp cấu hình và xác nhận trạng thái agent là `running`.
- Tạo request thử để phát sinh log và kiểm tra trên CloudWatch.

### 4.6. S3 sao lưu dữ liệu

- Tạo S3 bucket riêng tư.
- Bật Block Public Access.
- Bật mã hóa mặc định cho các object.
- Tổ chức object theo ngày, ví dụ `mongodb-backups/2026-09-16/`.
- Xuất dữ liệu bằng MongoDB Compass hoặc `mongodump`.
- Tải các tệp sao lưu lên S3.
- Thiết lập Lifecycle Rule cho những bản sao cũ.
- Thực hiện restore thử trên môi trường kiểm tra.

### 4.7. Kiểm thử nghiệm thu

- DNS của ALB trả về HTTP 200.
- Cả hai target đều có trạng thái `Healthy`.
- Khi dừng Backend trên một EC2, hệ thống vẫn phản hồi qua EC2 còn lại.
- Log của cả hai EC2 xuất hiện trong CloudWatch.
- Một bản sao tải từ S3 được khôi phục thử thành công.
- Cổng 8080 không thể truy cập trực tiếp từ Internet.

---

## 5. Lộ trình & mốc triển khai


Dự án dự kiến được triển khai trong **tối thiểu 8 tuần, tương đương khoảng 2 tháng hoặc 40 ngày làm việc**, tính từ ngày bắt đầu được thống nhất. Lộ trình áp dụng cho phạm vi triển khai hạ tầng AWS trên mã nguồn Backend hiện có. Các mốc dưới đây là kế hoạch dự kiến, không phải xác nhận công việc đã hoàn thành; ngày bắt đầu và kết thúc cụ thể sẽ được cập nhật khi chốt lịch triển khai.

| Giai đoạn | Tuần 1 | Tuần 2 | Tuần 3 | Tuần 4 | Tuần 5 | Tuần 6 | Tuần 7 | Tuần 8 |
|---|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| 1. Khảo sát và thiết kế | ● | ● | | | | | | |
| 2. Triển khai EC2 nền tảng | | ● | ● | | | | | |
| 3. Cấu hình cân bằng tải | | | ● | ● | | | | |
| 4. Bổ sung EC2 thứ hai | | | | ● | | | | |
| 5. Hoàn thiện quyền và giám sát | | | | | ● | | | |
| 6. Thiết lập sao lưu dữ liệu | | | | | ● | ● | | |
| 7. Kiểm tra khôi phục | | | | | | ● | | |
| 8. Kiểm thử, tối ưu và nghiệm thu kỹ thuật | | | | | | ● | ● | |
| 9. Hoàn thiện tài liệu và bàn giao | ● | ● | ● | ● | ● | ● | ● | ● |

**Ký hiệu:** ● là tuần thực hiện. Tài liệu và bằng chứng triển khai được cập nhật xuyên suốt. Tuần cuối được dành cho bàn giao, kiểm thử lại và xử lý các vấn đề còn tồn đọng.

---

## 6. Ước tính ngân sách

Chi phí thực tế phụ thuộc vào loại instance, thời gian hoạt động, dung lượng log, dung lượng sao lưu và lưu lượng truy cập.

Các nguồn phát sinh chi phí chính gồm:

| Hạng mục | Cơ sở tính chi phí | Biện pháp kiểm soát chi phí |
|---|---|---|
| Amazon EC2 | Hai instance nhân với số giờ hoạt động | Chọn instance nhỏ phù hợp tải; dừng môi trường thực hành khi không sử dụng nếu không yêu cầu sẵn sàng liên tục |
| EBS và AMI Snapshot | Dung lượng volume và snapshot theo tháng | Xóa AMI và snapshot thử nghiệm không còn sử dụng |
| Elastic IP/Public IPv4 | Số địa chỉ IPv4 công khai và thời gian sử dụng | Chỉ duy trì địa chỉ cần thiết và giải phóng khi không còn sử dụng |
| Application Load Balancer | Số giờ hoạt động và Load Balancer Capacity Units | Theo dõi lưu lượng; ALB có thể là khoản chi phí đáng kể với hệ thống nhỏ |
| Amazon CloudWatch | Dung lượng log ingest, lưu trữ và truy vấn | Đặt thời gian retention thay vì `Never expire` khi không cần lưu vĩnh viễn |
| Amazon S3 | Dung lượng lưu trữ, request và truy xuất dữ liệu | Dùng Lifecycle Rule và tránh lưu các bản sao trùng lặp |
| Data Transfer | Lưu lượng ra Internet và giữa các khu vực | Giữ tài nguyên AWS trong cùng Region khi có thể |
| MongoDB Atlas, Netlify, Cloudinary | Theo gói dịch vụ hiện tại | Không phát sinh chi phí chuyển đổi trong phạm vi đề xuất |

Để có con số chính xác, cần nhập cấu hình thực tế vào AWS Pricing Calculator theo Region Singapore, loại EC2, thời gian vận hành và mức sử dụng dự kiến.

Ngoài ra, nên tạo AWS Budget và cảnh báo chi phí để phát hiện sớm khi mức sử dụng vượt quá kế hoạch.

---

## 7. Đánh giá rủi ro

| Rủi ro | Mức ảnh hưởng | Biện pháp giảm thiểu |
|---|---|---|
| Hai EC2 cùng được tạo từ một cấu hình bị lỗi | Cao | Kiểm thử AMI trước khi nhân bản, quản lý phiên bản và chuẩn bị quy trình rollback |
| Health check trả về HTTP 200 nhưng chức năng quan trọng vẫn bị lỗi | Cao | Xây dựng endpoint `/health` riêng; `/stories` chỉ nên được sử dụng trong giai đoạn kiểm tra ban đầu |
| MongoDB Atlas không cho phép kết nối từ EC2 mới | Cao | Cập nhật Network Access có kiểm soát và không mở phạm vi lớn hơn cần thiết |
| Session hoặc tệp cục bộ không đồng bộ giữa hai EC2 | Cao | Sử dụng stateless session hoặc kho lưu trữ dùng chung |
| Các cổng 80, 22 hoặc 8080 được mở quá rộng | Cao | ALB mở cổng 80; EC2 nhận cổng 80 từ ALB Security Group; SSH giới hạn IP; không công khai cổng 8080 |
| IAM Role có quyền quá lớn | Cao | Tách policy theo nhiệm vụ, giới hạn bucket/prefix và rà soát quyền định kỳ |
| Log tăng nhanh gây phát sinh chi phí | Trung bình | Đặt thời gian retention và loại bỏ các log không cần thiết |
| Bản sao S3 bị công khai hoặc không thể khôi phục | Cao | Bật Block Public Access, mã hóa, áp dụng least privilege và restore thử |
| Tài nguyên tiếp tục phát sinh chi phí sau khi không còn sử dụng | Trung bình | Gắn tag, tạo AWS Budget và xóa tài nguyên thử nghiệm |
| Kiến trúc chưa tự động tạo EC2 thay thế | Trung bình | Trong giai đoạn sau có thể bổ sung Launch Template và Auto Scaling Group |
| Hệ thống chỉ sử dụng HTTP nên dữ liệu truyền chưa được mã hóa | Cao | Trong giai đoạn sản xuất cần bổ sung domain, AWS Certificate Manager và Listener HTTPS:443 |

---

## 8. Kết quả kỳ vọng

Sau khi hoàn thành triển khai, hệ thống dự kiến đạt được các kết quả sau:

- Backend hoạt động trên hai EC2, giảm phụ thuộc vào một máy chủ duy nhất.
- Người dùng truy cập API qua một DNS name chung của ALB.
- Request được phân phối đến một trong hai target đang có trạng thái `Healthy`.
- Khi một target gặp lỗi, ALB ngừng gửi lưu lượng đến target đó.
- Node.js chỉ lắng nghe nội bộ tại `127.0.0.1:8080`.
- Nginx tiếp nhận lưu lượng tại cổng 80 và chuyển tiếp vào ứng dụng.
- Log output và error của mỗi EC2 được tập trung trong CloudWatch.
- EC2 truy cập CloudWatch và S3 bằng IAM Role thay vì Access Key cục bộ.
- Bản sao MongoDB được lưu trong S3 bucket riêng tư.
- Có quy trình kiểm tra khả năng khôi phục dữ liệu từ bản sao.
- Kiến trúc có thể tiếp tục mở rộng bằng HTTPS, Auto Scaling Group, Route 53 và hệ thống triển khai tự động.

Các tiêu chí nghiệm thu tối thiểu gồm:

- Hai target có trạng thái `Healthy`.
- Endpoint thông qua ALB trả về HTTP 200.
- Hệ thống vẫn hoạt động khi dừng một Backend.
- Log của hai EC2 xuất hiện trong CloudWatch.
- Một bản sao trên S3 được restore thử thành công.
- Cổng 8080 không thể truy cập trực tiếp từ Internet.

---

## Kết luận

Giải pháp sử dụng **Amazon EC2, Elastic IP, Application Load Balancer, Target Group, AWS IAM, Amazon CloudWatch và Amazon S3** để xây dựng lớp hạ tầng Backend có khả năng phân phối tải, giám sát tập trung và hỗ trợ sao lưu cho Web Truyện Tranh.

Thiết kế giữ nguyên Frontend trên Netlify, MongoDB Atlas và Cloudinary để tận dụng các thành phần đang hoạt động ổn định. Phạm vi triển khai tập trung vào những vấn đề thực tế của Backend gồm điểm lỗi đơn, địa chỉ quản trị không ổn định, thiếu cân bằng tải, thiếu health check, quản lý quyền, log phân tán và sao lưu dữ liệu.

Các dịch vụ được sử dụng có quan hệ chức năng rõ ràng:

- Amazon EC2 chạy ứng dụng Backend.
- Elastic IP cung cấp địa chỉ IP quản trị ổn định.
- Application Load Balancer tiếp nhận và phân phối request.
- Target Group quản lý EC2 và thực hiện health check.
- AWS IAM kiểm soát quyền truy cập dịch vụ.
- Amazon CloudWatch tập trung log và hỗ trợ giám sát.
- Amazon S3 lưu trữ các bản sao dữ liệu MongoDB.

Đây là nền tảng phù hợp để tiếp tục bổ sung HTTPS, Route 53 và Auto Scaling Group khi hệ thống chuyển sang giai đoạn vận hành thực tế.
