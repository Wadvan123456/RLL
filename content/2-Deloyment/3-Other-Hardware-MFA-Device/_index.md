---
title: "Launch EC2 Instances"
date: "2025-08-13"
weight: 3
chapter: false
pre: " <b> 2.3 </b> "
---

## Launch EC2 Instances for the RL Platform — Hướng dẫn chi tiết

Amazon EC2 cung cấp máy chủ ảo linh hoạt, có thể mở rộng để chạy các workload huấn luyện và suy luận Reinforcement Learning.

---

### 1. Đăng nhập vào AWS Management Console

- Truy cập https://console.aws.amazon.com/ec2
- Đăng nhập tài khoản AWS đã có quyền phù hợp.

---

### 2. Mở dịch vụ EC2

- Trong menu **Services**, tìm kiếm và chọn **EC2** để vào bảng điều khiển quản lý EC2.

---

### 3. Bắt đầu tạo Instance mới

- Nhấn nút **Launch Instance** để bắt đầu cấu hình máy chủ ảo mới.

---

### 4. Chọn Amazon Machine Image (AMI)

- AMI là bản image hệ điều hành và phần mềm sẵn có.
- Một số lựa chọn phổ biến:
  - **Amazon Linux 2**: nhẹ, tích hợp tốt với AWS.
  - **Ubuntu Server**: phổ biến, hỗ trợ nhiều phần mềm.
  - **Deep Learning AMI**: đã cài sẵn các framework AI như TensorFlow, PyTorch, rất tiện cho RL.

*Lưu ý:* Chọn AMI phù hợp với workload RL của bạn, đặc biệt nếu cần GPU hoặc các thư viện đặc thù.

---

### 5. Chọn Instance Type

- Dựa trên nhu cầu tính toán:
  - CPU intensive: loại `c5`, `m5`.
  - GPU để huấn luyện RL nhanh: loại `p3`, `g4dn`.
- Xem thông số kỹ thuật (CPU, RAM, GPU, băng thông) để chọn phù hợp.

---

### 6. Cấu hình chi tiết Instance

- **Network:** Chọn VPC đã tạo (ví dụ `RL-Platform-VPC`).
- **Subnet:** Chọn subnet trong VPC (public hoặc private tùy mục đích).
- **Auto-assign Public IP:** Bật nếu bạn cần truy cập instance qua Internet.
- **IAM Role:** Gán role đã tạo (ví dụ `EC2-RL-Platform-Role`) để cấp quyền truy cập tài nguyên AWS.
- **Shutdown behavior:** Đặt là Stop hoặc Terminate tùy chính sách.
- **User Data:** Có thể viết script bash để tự động cài đặt phần mềm, cập nhật khi khởi động instance (ví dụ: cài Python, thư viện RL).

---

### 7. Thêm Storage (EBS Volumes)

- Định nghĩa dung lượng ổ đĩa (SSD, HDD) cần thiết.
- Có thể thêm nhiều volume nếu muốn tách dữ liệu và hệ thống.
- Chọn loại EBS phù hợp: General Purpose SSD (gp3), Provisioned IOPS (io2) nếu cần hiệu năng cao.

---

### 8. Cấu hình Security Group (Tường lửa)

- Tạo hoặc chọn Security Group.
- Thiết lập rules inbound:
  - Mở cổng **SSH (22)** chỉ cho IP của bạn để bảo mật.
  - Mở cổng khác nếu ứng dụng RL cần (ví dụ cổng HTTP, HTTPS).
- Rules outbound mặc định thường mở toàn bộ.

---

### 9. Kiểm tra lại và khởi chạy

- Review toàn bộ thiết lập.
- Chọn hoặc tạo **Key Pair** để đăng nhập SSH vào instance:
  - Tải file `.pem` về và lưu kỹ, dùng để kết nối.
- Nhấn **Launch** để tạo instance.

---

### Các lưu ý và Best Practices

- **Spot Instances:** Nếu muốn tiết kiệm chi phí, dùng Spot Instances nhưng lưu ý có thể bị AWS thu hồi bất ngờ.
- **Monitoring:** Kích hoạt Amazon CloudWatch để theo dõi CPU, RAM, đĩa, mạng.
- **Auto Scaling:** Sau này có thể cấu hình nhóm Auto Scaling để tự động tăng giảm số lượng instance.
- **Automation:** Sử dụng User Data scripts hoặc công cụ cấu hình (Ansible, Terraform) để tự động hóa việc tạo và cấu hình instance.

---

### Ví dụ User Data Script (bash) tự động cài đặt Python và thư viện RL

```bash
#!/bin/bash
yum update -y
yum install -y python3 git
pip3 install --upgrade pip
pip3 install tensorflow gym ray[rllib]
