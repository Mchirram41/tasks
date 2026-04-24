

# AWS IAM & EC2 S3 Access Setup

## 📌 Overview

This project demonstrates how to:

* Create IAM users: **Developer, Tester, Admin**
* Attach policies for **S3 and EC2 access**
* Assign an **IAM Role to EC2** for accessing S3 buckets

---

## 🛠️ Prerequisites

* AWS Account
* Access to AWS Console
* Basic understanding of IAM and EC2

---

## 👤 Step 1: Create IAM Users

1. Go to IAM → Users → Create User
2. Create the following users:

   * Developer
   * Tester
   * Admin
3. Enable **Console access** (optional)
4. Set password and permissions later

---

## 🔐 Step 2: Create IAM Group

1. Go to IAM → User Groups → Create group
2. Group name: `multiuser`
3. Add users:

   * Developer
   * Tester
   * Admin

---

## 📜 Step 3: Attach Policies (S3 & EC2)

### Option 1: Attach AWS Managed Policies (Quick Setup)

* AmazonS3FullAccess
* AmazonEC2FullAccess

Attach these policies to the **multiuser group**

---

### Option 2: (Recommended - Least Privilege)

Create a custom policy:

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": ["s3:ListBucket", "s3:GetObject", "s3:PutObject"],
      "Resource": "*"
    },
    {
      "Effect": "Allow",
      "Action": ["ec2:DescribeInstances", "ec2:StartInstances", "ec2:StopInstances"],
      "Resource": "*"
    }
  ]
}
```

Attach this policy to the **multiuser group**

---

## 🖥️ Step 4: Create IAM Role for EC2

1. Go to IAM → Roles → Create role
2. Select **AWS Service → EC2**
3. Attach policy:

   * AmazonS3FullAccess *(or custom policy)*
4. Role name: `ec2-s3-access-role`

---

## 🔗 Step 5: Attach Role to EC2

1. Go to EC2 → Instances
2. Select your instance
3. Click: **Actions → Security → Modify IAM Role**
4. Select: `ec2-s3-access-role`
5. Save changes

---

## ✅ Step 6: Verify Access

SSH into EC2 and run:

```bash
aws s3 ls
```

If S3 buckets are listed → ✅ Access is working

---

## 🧠 Key Concepts

* **IAM Users** → Human access
* **IAM Groups** → Manage permissions centrally
* **IAM Role** → Used by AWS services (like EC2)
* **Instance Profile** → Connects IAM Role to EC2

---

## ⚡ Best Practices

* Avoid full access policies in production
* Follow **least privilege principle**
* Enable **MFA for all users**
* Use **roles instead of access keys** for EC2

---

## 🎯 Conclusion

This setup ensures:

* Secure user access via IAM
* Controlled permissions using groups
* Seamless EC2 to S3 communication using IAM roles

---
