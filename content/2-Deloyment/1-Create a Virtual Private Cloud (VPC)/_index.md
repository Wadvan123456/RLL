---
title: "Create a Virtual Private Cloud (VPC)"
date: "2025-08-13"
weight: 1
chapter: false
pre: " <b> 2.1 </b> "
---

## Tạo Virtual Private Cloud (VPC) trên AWS – Hướng dẫn chi tiết

Virtual Private Cloud (VPC) là mạng riêng ảo trong AWS, cho phép bạn kiểm soát hoàn toàn môi trường mạng, như dải IP, subnet, route table, gateway… giúp bảo mật và tối ưu hạ tầng.

---

### Bước 1: Đăng nhập AWS Management Console

- Truy cập [https://aws.amazon.com/console](https://aws.amazon.com/console) và đăng nhập tài khoản AWS của bạn.

---

### Bước 2: Mở dịch vụ VPC

- Tại thanh tìm kiếm trên cùng (Search Services), gõ **VPC** và chọn dịch vụ **VPC**.

---

### Bước 3: Bắt đầu tạo VPC mới

- Trong bảng điều khiển (VPC Dashboard), bấm **Create VPC** (nút màu xanh bên phải).

---

### Bước 4: Cấu hình thông số cho VPC

- **Name tag:** Nhập tên cho VPC, ví dụ `RL-Platform-VPC`.

- **IPv4 CIDR block:** Nhập dải IP cho VPC, ví dụ `10.0.0.0/16`.  
  > Đây là dải mạng riêng, bạn có thể tùy chỉnh nhưng phải tuân thủ chuẩn CIDR. Dải này cho phép 65,536 địa chỉ IP.

- **IPv6 CIDR block (optional):**  
  - Nếu bạn muốn hỗ trợ IPv6, chọn **Amazon-provided IPv6 CIDR block** hoặc bỏ qua nếu không cần.

- **Tenancy:**  
  - Chọn **Default** (shared hardware) thường dùng cho hầu hết ứng dụng.  
  - Chọn **Dedicated** nếu muốn tài nguyên vật lý dành riêng, chi phí cao hơn.

![VPC](images/1.png)

---

### Bước 5: Tạo VPC

- Bấm nút **Create VPC** bên dưới để tạo.

- Hệ thống sẽ hiện thông báo thành công cùng các thông tin VPC bạn vừa tạo.

---

### Bước 6: Tạo Subnets (Mạng con)

- Trong menu bên trái, chọn **Subnets**.

- Bấm **Create subnet**.

- **Tên subnet:** Ví dụ `Public-Subnet-1`.

- **VPC:** Chọn VPC bạn vừa tạo (`RL-Platform-VPC`).

- **Availability Zone:** Chọn AZ (ví dụ `us-east-1a`).

- **IPv4 CIDR block:** Nhập dải nhỏ hơn nằm trong dải của VPC, ví dụ `10.0.1.0/24` (có 256 địa chỉ).

- Nhấn **Create subnet**.

- Tương tự, tạo thêm subnet private với CIDR block khác, ví dụ `10.0.2.0/24`.

![VPC](images/3.png)

---

### Bước 7: Tạo Internet Gateway (IGW)

- Chọn **Internet Gateways** trên menu bên trái.

- Bấm **Create internet gateway**.

- Đặt tên (Tag) như `RL-Platform-IGW`.

- Bấm **Create internet gateway**.

- Sau đó, chọn Internet Gateway vừa tạo, bấm **Actions** → **Attach to VPC**.

- Chọn `RL-Platform-VPC` → **Attach internet gateway**.

---

### Bước 8: Cấu hình Route Table (Bảng định tuyến)

- Chọn **Route Tables** trong menu.

- Chọn bảng route mặc định của VPC (bảng route sẽ có tên VPC).

- Bấm tab **Routes** → **Edit routes**.

- Thêm route:  
  - Destination: `0.0.0.0/0` (tất cả lưu lượng IPv4)  
  - Target: chọn Internet Gateway (`igw-xxxxx`) vừa tạo.

- Lưu lại.

---

### Bước 9: Liên kết Route Table với Subnet Public

- Vẫn ở bảng route, bấm tab **Subnet Associations**.

- Bấm **Edit subnet associations**.

- Chọn subnet `Public-Subnet-1` để liên kết.

- Lưu lại.

---

### Bước 10: Tạo Security Groups (Nhóm bảo mật)

- Vào **Security Groups** trên menu bên trái.

- Bấm **Create security group**.

- Đặt tên ví dụ: `RL-Platform-SG-Public`.

- Gán vào VPC `RL-Platform-VPC`.

- Trong phần **Inbound rules**:

  - Thêm rule cho phép SSH (port 22) từ IP của bạn (ví dụ `YOUR_IP/32`) để bảo mật.

  - Cho phép HTTP (port 80), HTTPS (port 443) từ mọi nơi (`0.0.0.0/0`).

- Lưu rule.

![VPC](images/4.png)
---

### Bước 11: Hoàn thiện và kiểm tra

- Bạn đã có VPC với:

  - Một dải mạng lớn (`10.0.0.0/16`).

  - Subnet public có Internet Gateway và route table.

  - Security Group cho phép truy cập cần thiết.

- Bạn có thể dùng VPC này để khởi tạo EC2 instances, kết nối an toàn trong RL platform.

---

## Lưu ý quan trọng

- CIDR block cho VPC và subnet phải không được trùng với mạng on-premises nếu bạn thiết lập VPN.

- Tận dụng nhiều Availability Zone để tăng độ sẵn sàng.

- Luôn cấu hình Security Group chặt chẽ theo nguyên tắc least privilege.

---


