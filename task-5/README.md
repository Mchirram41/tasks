
# AWS Transit Gateway Setup 

## 🌐 Overview

AWS Transit Gateway acts as a **central hub** that connects:

* Multiple VPCs
* On-premises networks (via VPN/Direct Connect)

👉 Instead of creating multiple VPC peering connections, TGW simplifies networking using a **hub-and-spoke model**

---

## 🛠️ Prerequisites

* AWS Account
* At least **2 VPCs** created
* Subnets in each VPC
* Basic understanding of VPC networking

---

## 🏗️ Architecture

```
        VPC-A
          |
          |
        TGW
       /   \
      /     \
  VPC-B     VPC-C
```

---

## 🚀 Step 1: Create Transit Gateway

1. Go to **VPC Dashboard**
2. Click **Transit Gateways**
3. Click **Create Transit Gateway**

### Configuration:

* **Name**: `my-transit-gateway`
* Keep defaults (Auto accept shared attachments, DNS support enabled)

Click **Create Transit Gateway**

---

## 🔗 Step 2: Create VPC Attachments

### Attach VPC-A:

1. Go to **Transit Gateway Attachments**
2. Click **Create attachment**
3. Select:

   * Resource type: **VPC**
   * Choose **VPC-A**
   * Select subnets (at least one per AZ)
4. Click **Create attachment**

---

### Attach VPC-B:

Repeat same steps for **VPC-B**

---

## 🔄 Step 3: Update Route Tables

### In VPC-A Route Table:

* Add route:

```
Destination: VPC-B CIDR
Target: Transit Gateway
```

### In VPC-B Route Table:

* Add route:

```
Destination: VPC-A CIDR
Target: Transit Gateway
```

---

## 🔐 Step 4: Configure Security Groups

* Allow required traffic (e.g., ICMP/SSH) between VPCs
* Example:

  * Allow **ICMP (ping)** for testing
  * Allow **port 22 (SSH)** if needed

---

## 🧪 Step 5: Test Connectivity

1. Launch EC2 instances in both VPCs
2. SSH into one instance
3. Ping the private IP of another instance

```bash
ping <private-ip>
```

✅ Expected Result: Ping should work

---

## 🧠 Key Concepts

* **Transit Gateway (TGW)** → Central router for VPCs
* **Attachment** → Connects VPC to TGW
* **Route Table** → Controls traffic flow
* **Hub-and-Spoke Model** → Scalable architecture

---

## ⚡ Benefits of Transit Gateway

* Simplifies network architecture
* Reduces number of peering connections
* Supports hybrid connectivity (VPN/Direct Connect)
* Centralized routing management

---

## 🔥 Best Practices

* Use **separate route tables** for segmentation
* Enable **flow logs** for monitoring
* Use **least privilege security groups**
* Plan CIDR ranges to avoid overlap

---

## 🎯 Conclusion

AWS Transit Gateway helps:

* Connect multiple VPCs efficiently
* Simplify complex network architectures
* Enable scalable and secure communication

---

## 📚 Interview Tip

> “Transit Gateway is used to centrally connect multiple VPCs and on-prem networks using a hub-and-spoke model, reducing the complexity compared to VPC peering.”

---
