---
title: "Công tác chuẩn bị"
date: "2026-07-10"
weight: 1
chapter: false
pre: "<b> 5.1 </b>"
---


### Yêu cầu

Trước khi bắt đầu thiết kế và triển khai hạ tầng cho hệ thống **Website Truyện Tranh trên AWS**, cần chuẩn bị đầy đủ tài khoản, công cụ, mã nguồn và môi trường phát triển.

Các yêu cầu cần chuẩn bị bao gồm:

---

### 1. Tài khoản AWS

Cần có một **tài khoản AWS (Amazon Web Services)** để tạo và quản lý các tài nguyên Cloud được sử dụng trong Workshop.

Trong quá trình triển khai, tài khoản AWS sẽ được sử dụng để làm việc với các dịch vụ như:

- **Amazon EC2**: Khởi tạo máy chủ để triển khai ứng dụng.
- **Amazon S3**: Lưu trữ dữ liệu và các tài nguyên tĩnh khi cần thiết.
- **Amazon CloudWatch**: Theo dõi hoạt động của hệ thống.
- **AWS IAM**: Quản lý quyền truy cập vào các tài nguyên AWS.
- Các dịch vụ AWS khác được bổ sung trong quá trình xây dựng hệ thống.

> **Lưu ý:** Hạn chế sử dụng tài khoản Root cho các thao tác triển khai thông thường. Nên sử dụng IAM User hoặc IAM Role với các quyền phù hợp.

---

### 2. Hoàn thành các nhiệm vụ nhận AWS Credits(Không bắt buộc)

Trong phạm vi chương trình thực tập, cần hoàn thành các nhiệm vụ được yêu cầu để nhận **AWS Credits**.

AWS Credits được sử dụng để hỗ trợ chi phí cho việc tạo và vận hành các tài nguyên AWS trong quá trình thực hiện Workshop.

Trước khi triển khai cần kiểm tra:

- AWS Credits đã được cộng vào tài khoản.
- Số Credits hiện có.
- Thời hạn sử dụng của Credits.
- Các dịch vụ có thể sử dụng Credits.
- Theo dõi chi phí trong quá trình triển khai.

> **Khuyến nghị:** Nên thiết lập **AWS Budget** và cảnh báo chi phí để hạn chế trường hợp tài nguyên AWS phát sinh chi phí ngoài dự kiến.

---

### 3. Project Website có sẵn

Workshop yêu cầu một **Project Website có sẵn** để thực hiện quá trình triển khai lên hạ tầng AWS.

Project nên có tối thiểu:

- Frontend của Website.
- Backend cung cấp REST API.
- Database hoặc kết nối tới Database.
- File cấu hình các biến môi trường.
- Source Code được quản lý bằng Git.
- Có khả năng chạy thành công trên môi trường Local trước khi triển khai lên AWS.

Trong Workshop này, Project được sử dụng là một **Website Truyện Tranh**, bao gồm Frontend, Backend và Database.

Nếu chưa có Project riêng, có thể sử dụng Project mẫu được cung cấp dưới đây để thực hành:

**Source Code Project:**  
[Website Truyện Tranh - GitHub](LINK_GITHUB_PROJECT_CUA_BAN)

> **Lưu ý:** Thay `LINK_GITHUB_PROJECT_CUA_BAN` bằng đường dẫn GitHub của Project trước khi hoàn thiện báo cáo.

Trước khi tiếp tục, cần đảm bảo Project có thể chạy bình thường trên máy tính cá nhân. Điều này giúp phân biệt các lỗi của ứng dụng với các lỗi phát sinh trong quá trình cấu hình hạ tầng AWS.

---

### 4. Trình duyệt Google Chrome

Cần cài đặt **Google Chrome** để truy cập và quản lý các nền tảng được sử dụng trong Workshop như:

- AWS Management Console.
- MongoDB Atlas.
- GitHub.
- Website sau khi triển khai.
- Các công cụ quản lý và kiểm thử khác.

Nên sử dụng phiên bản Google Chrome mới để đảm bảo khả năng tương thích với AWS Management Console và các dịch vụ Web hiện đại.

---

### 5. Node.js(Nếu bạn đã có sẵn mã nguồn project từ trước thì không cần làm bước này)

Cần cài đặt **Node.js** trên máy tính cá nhân để chạy và kiểm thử Project trước khi triển khai.

Có thể kiểm tra phiên bản Node.js bằng lệnh:

```bash
node --version
```

Kiểm tra phiên bản npm:

```bash
npm --version
```

Node.js và npm được sử dụng để:

- Chạy Backend trên môi trường Local.
- Cài đặt các package cần thiết.
- Build Project.
- Kiểm thử ứng dụng trước khi triển khai.
- Kiểm tra và xử lý lỗi trong quá trình phát triển.

> **Khuyến nghị:** Nên sử dụng phiên bản Node.js LTS hoặc phiên bản tương thích với Project đang sử dụng.

---

### 6. Tài khoản MongoDB Atlas

Hệ thống sử dụng **MongoDB Atlas** làm cơ sở dữ liệu, vì vậy cần chuẩn bị một tài khoản MongoDB Atlas.

Sau khi đăng ký tài khoản, cần thực hiện các bước cơ bản:

1. Tạo MongoDB Project.
2. Tạo Database Cluster.
3. Tạo Database User.
4. Thiết lập Network Access.
5. Lấy MongoDB Connection String.
6. Cấu hình Connection String vào biến môi trường của Backend.

Ví dụ:

```env
MONGODB_URI=mongodb+srv://<username>:<password>@<cluster>/<database>
```

> **Lưu ý:** Không đưa username, password, Connection String hoặc các thông tin bảo mật trực tiếp lên GitHub.

Nếu Project đã có sẵn MongoDB Atlas Cluster, có thể tiếp tục sử dụng Cluster hiện tại và chỉ cần kiểm tra lại cấu hình Network Access trước khi triển khai Backend lên AWS.

---

### 7. Máy tính cá nhân

Cần chuẩn bị một máy tính hoặc laptop có cấu hình cơ bản để thực hiện Workshop.

Cấu hình đề xuất:

| Thành phần | Yêu cầu |
|---|---|
| CPU | Intel Core i3 / AMD Ryzen 3 hoặc tương đương trở lên |
| RAM | Tối thiểu 8 GB |
| Ổ cứng | Còn trống tối thiểu 10 GB |
| Hệ điều hành | Windows 10/11, Linux hoặc macOS |
| Internet | Kết nối Internet ổn định |
| Trình duyệt | Google Chrome |
| Node.js | Phiên bản phù hợp với Project |

Workshop chủ yếu triển khai và vận hành tài nguyên trên AWS nên không yêu cầu máy tính cá nhân có cấu hình quá cao.

Máy tính cá nhân chủ yếu được sử dụng để:

- Chỉnh sửa Source Code.
- Chạy thử ứng dụng trên Local.
- Truy cập AWS Management Console.
- SSH vào máy chủ EC2.
- Quản lý Source Code.
- Kiểm thử hệ thống sau khi triển khai.

---

### 8. Các công cụ hỗ trợ

Ngoài các yêu cầu chính, nên chuẩn bị thêm một số công cụ hỗ trợ quá trình phát triển và triển khai:

- **Visual Studio Code** hoặc IDE tương đương để chỉnh sửa Source Code.
- **Git** để quản lý phiên bản mã nguồn.
- **GitHub** để lưu trữ Source Code.
- **Postman** để kiểm thử REST API.
- **PowerShell / Terminal** để thực hiện các câu lệnh.
- **SSH Client** để kết nối tới máy chủ EC2.

Có thể kiểm tra Git bằng lệnh:

```bash
git --version
ssh -V
```

---

### 9. Kết quả cần đạt được

Sau khi hoàn thành bước chuẩn bị, cần đảm bảo:

- Có tài khoản AWS và có thể truy cập AWS Management Console.
- Đã hoàn thành các nhiệm vụ cần thiết để nhận AWS Credits.
- Có đủ AWS Credits phục vụ quá trình thực hành.
- Có máy tính đáp ứng cấu hình cơ bản.
- Đã cài đặt Google Chrome.
- Đã cài đặt Node.js và npm.
- Có tài khoản MongoDB Atlas.
- Có Database Cluster phục vụ cho Project.
- Có Git và GitHub để quản lý Source Code.
- Có một Project Website để triển khai.
- Project có thể chạy thành công trên môi trường Local.
- Có thể sử dụng Project mẫu được cung cấp nếu chưa có Project riêng.

> **Note:**  
> Nếu đã có sẵn một Project hoàn chỉnh và Project có thể chạy ổn định trên môi trường Local, bạn có thể **bỏ qua các bước cài đặt và cấu hình môi trường phát triển đã có sẵn**, chẳng hạn như Node.js, npm, Git, GitHub và MongoDB Atlas.  
>
> Tuy nhiên, cần đảm bảo Project đã hoạt động bình thường trước khi tiếp tục các bước triển khai lên AWS.

Sau khi hoàn thành các yêu cầu trên, có thể chuyển sang bước tiếp theo để bắt đầu **thiết kế và triển khai hạ tầng Website Truyện Tranh trên AWS**.