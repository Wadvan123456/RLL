---
title: "Cleanup Resources"
date: "2025-08-13"
weight: 5
chapter: false
pre: " <b> 5. </b> "
---


## 5. Cleanup Resources

After completing your Reinforcement Learning deployment and experiments on AWS, it is important to clean up your resources to avoid unnecessary charges and keep your environment tidy.

### Steps to Clean Up AWS Resources

1. **Terminate EC2 Instances**  
   - Go to the EC2 Dashboard.  
   - Select the instances you launched for your RL workloads.  
   - Click **Actions** → **Instance State** → **Terminate**.

2. **Delete S3 Buckets and Objects**  
   - Navigate to the S3 Console.  
   - Select the buckets created for your project.  
   - Delete all objects inside the buckets.  
   - Delete the buckets themselves.

3. **Remove IAM Roles and Users**  
   - Open the IAM Console.  
   - Detach policies from roles and users created for the RL platform.  
   - Delete those roles, users, and groups if no longer needed.

4. **Delete Lambda Functions**  
   - In the Lambda Console, select functions used in your RL workflows.  
   - Delete the unnecessary functions.

5. **Clean Up Other Services**  
   - Delete any other AWS resources provisioned for your RL project, such as:  
     - CloudWatch log groups  
     - Step Functions state machines  
     - API Gateway endpoints  
     - VPCs, subnets, security groups (if dedicated to this project)

### Best Practices

- Regularly review your AWS account for unused resources.  
- Enable AWS Cost Explorer and set budget alerts to monitor your spending.  
- Automate cleanup with scripts or AWS tools like AWS CLI and CloudFormation stack deletions when possible.

---



