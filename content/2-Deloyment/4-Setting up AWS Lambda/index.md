---
title: "Set up AWS Lambda Functions"
date: "2025-08-13"
weight: 4
chapter: false
pre: " <b> 2.4 </b> "
---

## Setting up AWS Lambda Functions — Hướng dẫn chi tiết

AWS Lambda là dịch vụ tính toán serverless cho phép bạn chạy code mà không cần quản lý máy chủ. Lambda rất phù hợp để xử lý các event backend trong nền tảng RL của bạn.

---

### 1. Đăng nhập vào AWS Management Console

- Truy cập https://console.aws.amazon.com/lambda
- Đăng nhập tài khoản có quyền tạo Lambda.

---

### 2. Điều hướng đến dịch vụ Lambda

- Trong menu **Services**, tìm và chọn **Lambda**.

---

### 3. Tạo function mới

- Nhấn nút **Create function** để bắt đầu tạo hàm Lambda.

---

### 4. Chọn cách tạo function

- **Author from scratch:**  
  - Tên function ví dụ: `RL-DataProcessor`  
  - Runtime: Python 3.x, Node.js, Java, hoặc runtime phù hợp với code bạn muốn chạy.  
  - Execution role: chọn role có quyền phù hợp hoặc tạo mới.

- **Use a blueprint:**  
  - Chọn mẫu có sẵn để nhanh chóng khởi tạo.

- **Browse serverless app repository:**  
  - Dùng app serverless cộng đồng.

---

### 5. Cấu hình chi tiết function

- **Function name:** ví dụ `RL-DataProcessor`  
- **Runtime:** Python 3.8 (hoặc phiên bản bạn cần)  
- **Permissions:**  
  - Tạo hoặc chọn IAM Role có quyền truy cập các dịch vụ AWS cần thiết như S3, CloudWatch.  
  - Role này quyết định Lambda có thể làm gì (đọc ghi S3, ghi log CloudWatch, ...).

---

### 6. Viết hoặc upload mã nguồn

- Bạn có thể viết trực tiếp trong AWS Console hoặc upload file ZIP chứa code.
- Ví dụ function Python đơn giản:

```python
def lambda_handler(event, context):
    print("Received event:", event)
    # Xử lý dữ liệu RL tại đây
    return {"statusCode": 200, "body": "Success"}
