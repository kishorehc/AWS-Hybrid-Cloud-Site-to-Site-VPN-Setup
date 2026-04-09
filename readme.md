# 🚀 AWS Hybrid Cloud Site-to-Site VPN Setup

![AWS](https://img.shields.io/badge/AWS-VPN-orange)
![DevOps](https://img.shields.io/badge/DevOps-Project-blue)
![Status](https://img.shields.io/badge/Status-Active-success)
![Region](https://img.shields.io/badge/Region-ap--south--1-yellow)

---

## 📌 Project Overview

This project demonstrates a fully functional **Site-to-Site VPN connection** between two AWS VPCs:

* **Cloud VPC (`on-cloud-vpc`)** – Simulates AWS cloud environment
* **On-Prem VPC (`on-prem-vpc`)** – Simulates on-premises data center

The setup enables **secure communication between EC2 instances** using an **IPSec VPN tunnel**, achieving reliable hybrid cloud connectivity.

---

## ✨ Key Features

* 🔐 Secure IPSec Site-to-Site VPN
* 🌐 Hybrid Cloud Architecture Simulation
* ⚙️ End-to-End AWS Networking Setup
* 🔁 Real-time connectivity validation (Ping tests)
* 📊 Monitoring using CloudWatch
* 🛠️ Troubleshooting guide included

---

## 🛠️ Tech Stack

* AWS VPC
* EC2
* Site-to-Site VPN
* Virtual Private Gateway (VGW)
* Customer Gateway (CGW)
* CloudWatch
* Linux (Ubuntu)
* AWS CLI

---

## 🏗️ Architecture Diagram

```
Cloud VPC (172.3.0.0/16)        On-Prem VPC (10.0.0.0/16)
        │                                │
     EC2 Instance                    EC2 Instance
        │                                │
     Virtual Private Gateway      Customer Gateway
                │
        IPSec VPN Tunnel
```

---

## ⚙️ Step-by-Step Implementation

### Step 1: Create VPCs

* Cloud VPC CIDR: `172.3.0.0/16`
* On-Prem VPC CIDR: `10.0.0.0/16`
---

<img width="3718" height="1790" alt="Screenshot 2026-04-10 030546" src="https://github.com/user-attachments/assets/09c1dd47-e2cf-4b95-a247-9912f19b116b" />

---

### Step 2: Launch EC2 Instances

* Cloud Instance Private IP: `172.3.0.138`
* On-Prem Instance Private IP: `10.0.0.5`
---
<img width="3716" height="1771" alt="Screenshot 2026-04-10 030726" src="https://github.com/user-attachments/assets/cefe46e3-036c-4e73-b66f-37e040d8cb1a" />

---

### Step 3: Create Customer Gateway (CGW)

* Public IP: `65.1.85.37`
* ASN: `65000`
---
<img width="3701" height="1758" alt="Screenshot 2026-04-10 030620" src="https://github.com/user-attachments/assets/2aebfc43-0a8d-43e7-8d9d-ffeb5a5d4d6b" />

---

### Step 4: Create Virtual Private Gateway (VGW)

* Attach VGW to Cloud VPC
* ASN: `64512`
---
<img width="3712" height="1767" alt="Screenshot 2026-04-10 030644" src="https://github.com/user-attachments/assets/e626570e-5215-42e8-90c3-e87c3d2df348" />

---

### Step 5: Create VPN Connection

* Type: `ipsec.1`
* Connect CGW and VGW
---
<img width="3728" height="1799" alt="Screenshot 2026-04-10 030659" src="https://github.com/user-attachments/assets/35414270-17dc-4fa2-bc39-9c3a7592752f" />

---

### Step 6: Configure Route Tables

**Cloud VPC**

```
Destination: 10.0.0.0/16 → Target: VGW
```

**On-Prem VPC**

```
Destination: 172.3.0.0/16 → Target: CGW
```

---

### Step 7: Configure Security Groups

Allow the following:

* SSH (TCP 22)
* ICMP (Ping)
* UDP 500 (IPSec)
* UDP 4500 (NAT-T)

---

### Step 8: Test Connectivity

```bash
ping 172.3.0.138
ping google.com
```

---

## ✅ Test Results

| Test             | Source   | Destination | Result    |
| ---------------- | -------- | ----------- | --------- |
| VPN Connectivity | 10.0.0.5 | 172.3.0.138 | ✅ Success |
| Internet Access  | 10.0.0.5 | google.com  | ✅ Success |
| Packet Loss      | -        | -           | ✅ 0%      |

---

## 🛠️ Troubleshooting Guide

### ❌ VPN Tunnel Down

* Verify CGW & VGW states
* Check tunnel status
* Ensure UDP ports 500 & 4500 are open

---

### ❌ Unable to Ping

* Check route tables
* Allow ICMP in security groups
* Verify Network ACLs
* Ensure no overlapping CIDR

---

### ❌ SSH Permission Denied

```bash
chmod 400 key.pem
ssh -i key.pem ubuntu@<public-ip>
```

---

## 📊 Monitoring

Use AWS CloudWatch to monitor:

* Tunnel state
* Data transfer
* Packet count
* VPN metrics

---

## 🌍 Real-World Use Cases

* Hybrid cloud connectivity
* Secure enterprise networking
* Disaster recovery setups
* Extending on-prem networks to AWS

---

## 💰 Cost Estimation

| Service           | Estimated Cost |
| ----------------- | -------------- |
| VPN Connection    | ~$36/month     |
| VGW               | ~$36/month     |
| EC2 (2 instances) | ~$15/month     |
| **Total**         | **~$87/month** |

---

## 🔐 Security Best Practices

* Apply least privilege access
* Rotate VPN pre-shared keys
* Enable VPC Flow Logs
* Use bastion host for SSH
* Enable AWS CloudTrail

---

---

## 🚀 How to Reproduce

1. Create two VPCs
2. Launch EC2 instances
3. Create CGW and VGW
4. Establish VPN connection
5. Configure routing
6. Set security rules
7. Test connectivity

---

## 🎯 Resume Description

Designed and implemented a hybrid cloud architecture using AWS Site-to-Site VPN to securely connect on-premises and cloud environments, achieving reliable communication with 0% packet loss.

---

## 👤 Author

**Kishore HC**
DevOps Engineer

* Region: ap-south-1
* Environment: kishore_devops

---

## 📜 License

This project is for educational and demonstration purposes only.

---

## ✅ Status

✔ VPN Connection Active
✔ Stable Connectivity
✔ 0% Packet Loss

**Last Tested:** April 2026
