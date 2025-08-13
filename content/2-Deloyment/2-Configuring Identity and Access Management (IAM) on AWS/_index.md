---
title: "Configuring Identity and Access Management (IAM) on AWS"
date: "2025-08-13"
weight: 2
chapter: false
pre: " <b> 2.2 </b> "
---

## Configuring Identity and Access Management (IAM) on AWS — Hướng dẫn chi tiết

IAM là dịch vụ của AWS giúp bạn quản lý an toàn quyền truy cập và điều khiển ai có thể làm gì với các tài nguyên AWS của bạn. Việc cấu hình IAM đúng cách là bước quan trọng để bảo vệ hạ tầng Reinforcement Learning Platform của bạn.

---

### 1. Tạo IAM Users và Groups

- **IAM Users** là tài khoản riêng biệt cho người dùng hoặc ứng dụng, được cấp quyền truy cập cụ thể.
- **IAM Groups** là tập hợp các user có cùng vai trò công việc, giúp quản lý quyền dễ dàng hơn.

**Cách làm:**

1. Vào AWS Console → Services → IAM → Users → Add user.
2. Nhập tên user (ví dụ: `developer01`).
3. Chọn loại truy cập:
   - **Programmatic access** (API, CLI)
   - **AWS Management Console access** (giao diện web)
4. Tạo password hoặc để hệ thống tạo ngẫu nhiên.
5. Sau khi tạo user, tạo nhóm (Groups) nếu chưa có: IAM → Groups → Create group.
6. Thêm user vào nhóm theo vai trò (ví dụ: `Developers`, `Admins`).
![IAM](images/5.png)
---

### 2. Định nghĩa IAM Policies (Chính sách quyền)

- IAM Policies là các tập lệnh JSON xác định quyền nào được phép hoặc bị từ chối trên tài nguyên AWS.
- Có 2 loại chính:
  - **Managed policies:** do AWS cung cấp sẵn, dễ dùng.
  - **Customer managed policies:** do bạn tự tạo, tùy chỉnh cho nhu cầu riêng.

**Cách làm:**

1. IAM → Policies → Create policy.
2. Sử dụng trình soạn thảo visual hoặc nhập JSON.
3. Ví dụ: Policy cho phép EC2 full access, hoặc chỉ cho phép đọc S3.
4. Gán policy cho users, groups hoặc roles.

---

### 3. Tạo IAM Roles

- Roles cho phép cấp quyền tạm thời và cho các dịch vụ AWS (ví dụ EC2, Lambda) “mượn” quyền.
- Roles rất quan trọng để tránh dùng khóa truy cập cố định trong code.

**Cách làm:**

1. IAM → Roles → Create role.
2. Chọn type role, ví dụ: EC2, Lambda.
3. Chọn các policies phù hợp để gán (ví dụ: `AmazonS3ReadOnlyAccess`).
4. Đặt tên role dễ nhớ (ví dụ: `EC2-RL-Platform-Role`).
5. EC2 instance hoặc Lambda function sẽ sử dụng role này khi chạy.

---

### 4. Kích hoạt Multi-Factor Authentication (MFA)

- MFA tăng cường bảo mật bằng cách yêu cầu xác thực thêm ngoài mật khẩu, thường là mã OTP trên điện thoại.
- Bắt buộc cho user có quyền cao hoặc quyền truy cập console.

**Cách làm:**

1. IAM → Users → chọn user cần kích hoạt MFA.
2. Tab **Security credentials** → Manage MFA device.
3. Chọn thiết bị (ví dụ: Virtual MFA device dùng app Google Authenticator).
4. Quét mã QR và nhập mã OTP để kích hoạt.

---

### 5. Sử dụng IAM Access Analyzer

- Access Analyzer giúp bạn phát hiện xem IAM policies có thể làm lộ tài nguyên cho bên ngoài hoặc tài khoản khác không.

**Cách làm:**

1. IAM → Access Analyzer → Create analyzer.
2. Chọn vùng và tạo analyzer.
3. Xem báo cáo phân tích quyền truy cập, chỉnh sửa policies nếu cần để đảm bảo không lộ dữ liệu.

---

### 6. Kiểm toán và giám sát IAM Activities

- **AWS CloudTrail** giúp ghi lại toàn bộ hành động IAM và API gọi tới tài khoản AWS của bạn.
- **AWS Config** giúp kiểm tra cấu hình IAM có tuân thủ chính sách bảo mật hay không.
- **AWS Security Hub** tổng hợp và cảnh báo các vấn đề bảo mật.

**Cách làm:**

1. Bật CloudTrail cho toàn bộ tài khoản AWS (Services → CloudTrail).
2. Thiết lập AWS Config để theo dõi thay đổi trong IAM.
3. Sử dụng Security Hub để nhận cảnh báo tự động và đề xuất khắc phục.

---

### Best Practices (Thực hành tốt nhất)

- **Áp dụng nguyên tắc Least Privilege:** Cấp quyền chỉ đủ để người dùng hoàn thành nhiệm vụ, không thừa.
- **Thường xuyên đổi Access Keys:** Để tránh bị rò rỉ hoặc bị tấn công lâu dài.
- **Tránh dùng tài khoản root:** Chỉ dùng để thiết lập ban đầu; mọi công việc thường ngày nên dùng IAM users hoặc roles.
- **Dùng resource-based policies:** Khi có thể, để kiểm soát quyền trên tài nguyên thay vì user, giúp quản lý linh hoạt hơn.

---

