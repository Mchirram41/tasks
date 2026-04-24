
# AWS WAF + ALB Setup (Block Specific IP)

## 📌 Overview

This guide demonstrates how to:

* Attach a **WAF Web ACL** to an **Application Load Balancer (ALB)**
* Add a rule to **block traffic from a specific IP (your laptop)**
* Test application access **before and after** applying WAF rules

---

## 🛠️ Prerequisites

* AWS Account
* An existing **Application Load Balancer (ALB)** with a running application
* Public IP of your laptop (Google: *“what is my IP”*)

---

## 🌐 Step 1: Verify Application Access (Before WAF)

1. Go to **EC2 → Load Balancers**
2. Copy the **DNS name** of your ALB
   Example: `http://my-alb-123456.ap-south-1.elb.amazonaws.com`
3. Open in browser

✅ Expected Result:
Application should be **accessible**

---

## 🔐 Step 2: Create WAF Web ACL

1. Go to **AWS WAF & Shield**
2. Click **Web ACLs → Create web ACL**

### Configuration:

* **Name**: `block-ip-acl`
* **Region**: Same as ALB
* **Resource type**: **Regional resources**
* **Associate AWS resources**:

  * Select your **ALB**

Click **Next**

---

## 🚫 Step 3: Add Rule to Block IP

1. Click **Add rules → Add my own rules and rule groups**
2. Choose **Rule builder**

### Rule Configuration:

* **Rule name**: `block-my-ip`
* **Type**: IP set

---

### Create IP Set

1. Click **Create new IP set**

2. Name: `blocked-ip-set`

3. IP version: **IPv4**

4. Add your laptop IP:

   ```
   YOUR_IP/32
   ```

   Example:

   ```
   192.168.1.10/32
   ```

5. Save IP set

---

### Complete Rule Setup

* Select the created IP set
* **Action**: **Block**

Click **Add rule → Next**

---

## ⚙️ Step 4: Review & Create

* Keep default settings for logging/metrics (or enable if needed)
* Click **Create Web ACL**

---

## 🧪 Step 5: Test After WAF Applied

1. Open ALB URL again from your laptop

❌ Expected Result:

* You should see:

  * **403 Forbidden**
  * or **Request blocked**

---

## 🔄 Step 6: Re-Test (Optional)

* Remove your IP from IP set
  OR
* Change rule action to **Allow**

✅ Application should be accessible again

---

## 🧠 Key Concepts

* **WAF (Web Application Firewall)** → Protects web apps from unwanted traffic
* **Web ACL** → Collection of rules
* **IP Set** → List of IPs to allow/block
* **ALB Integration** → WAF filters traffic before reaching backend

---

## ⚡ Best Practices

* Use **IP blocking** for quick mitigation
* Prefer **managed rule groups** (AWS Managed Rules) for real-world security
* Enable **logging (CloudWatch / S3)** for monitoring
* Avoid blocking your own IP permanently (keep backup access)

---

## 🎯 Conclusion

This setup ensures:

* Controlled access to your application
* Ability to block malicious or unwanted IPs
* Improved security using AWS WAF with ALB

---
