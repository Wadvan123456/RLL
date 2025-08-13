---
title: "Configure Amazon S3 Buckets"
date: "2025-08-13"
weight: 5
chapter: false
pre: " <b> 2.5 </b> "
---

## Configure Amazon S3 Buckets

Amazon Simple Storage Service (S3) is an object storage service that offers industry-leading scalability, data availability, security, and performance. It is widely used to store data for websites, mobile apps, backup and restore, archive, enterprise applications, IoT devices, and big data analytics.

### 1. Create an S3 Bucket

- Sign in to the [AWS Management Console](https://console.aws.amazon.com/s3).
- Click **Create bucket**.
- Enter a globally unique **Bucket name**.
- Choose the **Region** closest to your users or your AWS resources.
- Configure options such as versioning, encryption, and tags if needed.
- Set **Bucket permissions** carefully to control public or private access.
- Click **Create bucket**.

### 2. Create Folders (Prefixes) within the Bucket

- Although S3 doesn’t have real folders, you can simulate them by using **prefixes**.
- When uploading objects, include the folder path in the key name (e.g., `logs/2025/08/13/logfile.txt`).
- You can also create empty folders in the AWS Console by creating a zero-byte object with a key ending with a slash (`folder-name/`).

### 3. Upload and Manage Data

- Upload files via the AWS Management Console, AWS CLI, or SDKs.
- To upload with CLI, use:
  ```bash
  aws s3 cp /local/path/file.txt s3://your-bucket-name/folder/
