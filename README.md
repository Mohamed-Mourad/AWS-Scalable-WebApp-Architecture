# Project 1: Scalable Web Application with ALB and Auto Scaling on AWS

## 📌 Overview

This project demonstrates **deploying a secure, scalable, and highly available EC2-based web application on AWS** using:

- **Application Load Balancer (ALB)**
- **Auto Scaling Groups (ASG)**
- **Multi-AZ RDS**
- **Public and Private Subnets**
- **Route 53 for DNS**
- **CloudWatch and SNS for monitoring and alerting**

following **AWS Well-Architected best practices**.

---

## 📈 Architecture Diagram

![Architecture Diagram](/webapp-architecture.png)

---

## 🛠️ Key AWS Services Used

- **VPC** with two Availability Zones (AZ-1, AZ-2)
- **Public and Private Subnets** for network segregation
- **Internet Gateway (IGW)** for inbound/outbound internet connectivity
- **NAT Gateways** for outbound internet access from private subnets
- **Route 53** for DNS routing
- **Application Load Balancer (ALB)** for distributing inbound HTTP/HTTPS traffic
- **Auto Scaling Group (ASG)** for automatic scaling and high availability of EC2 instances
- **EC2 Instances** for application hosting
- **Amazon RDS (Multi-AZ)** for managed relational database with automatic failover
- **CloudWatch and SNS** for monitoring, alerting, and auto scaling triggers
- **Security Groups** for layered security control

---

## 🪐 Architecture Breakdown

### **1️⃣ Networking**

- **VPC** spans **two Availability Zones** for high availability.
- **Public Subnets (AZ-1, AZ-2)**:
  - Contain **NAT Gateways** for outbound internet access from private subnets.
  - Host the **ALB**, which receives traffic from the internet via the IGW.
- **Private Subnets (AZ-1, AZ-2)**:
  - Host **EC2 instances** (web application servers).
  - Host **Amazon RDS Multi-AZ** (Primary in AZ-1, Secondary in AZ-2).

### **2️⃣ Internet Connectivity**

- An **Internet Gateway (IGW)** is attached to the VPC.
- **Route 53** routes `example.com` to the ALB, enabling user traffic to reach your application.

### **3️⃣ Load Balancing**

- **ALB** distributes incoming HTTP/HTTPS traffic across **EC2 instances** in private subnets.
- The ALB:
  - Is deployed across both public subnets for high availability.
  - Uses **Target Groups** to forward traffic to EC2 instances.

### **4️⃣ Auto Scaling**

- **Auto Scaling Groups (ASG)** manage EC2 instances:
  - Maintain desired capacity.
  - Scale out and in based on demand using **CloudWatch metrics**.
  - Replace unhealthy instances automatically.

### **5️⃣ Database Layer**

- **Amazon RDS Multi-AZ**:
  - Primary instance in AZ-1.
  - Secondary instance in AZ-2 for failover.
  - Ensures database high availability without manual intervention.

### **6️⃣ Outbound Internet Access**

- **NAT Gateways** in public subnets allow **EC2 instances in private subnets** to:
  - Download updates.
  - Access external APIs without exposing them to the public internet.

---

## 🔐 Security

- **Security Groups:**
  - ALB SG: Allow HTTP/HTTPS from the internet.
  - EC2 SG: Allow HTTP/HTTPS only from the ALB SG, no direct SSH (prefer SSM).
  - RDS SG: Allow database access only from EC2 SG.
- **Public/Private Subnet Separation**:
  - Only the ALB is exposed to the internet.
  - EC2 and RDS remain in isolated private networks.

---

## 📊 Monitoring and Alerting

- **Amazon CloudWatch**:
  - Collects metrics for EC2, ALB, and RDS.
  - Creates alarms for CPU usage, latency, unhealthy hosts, etc.
- **SNS (Simple Notification Service)**:
  - Sends notifications when CloudWatch alarms trigger.

---

## 🚀 Learning Outcomes

✅ Learned to deploy secure and scalable EC2-based applications on AWS.  
✅ Implemented high availability using **ALB, ASG, and Multi-AZ architecture**.  
✅ Optimized cost and performance using **Auto Scaling policies**.  
✅ Applied AWS security best practices using **VPC architecture, subnets, and security groups**.  
✅ Understood monitoring and alerting with **CloudWatch and SNS** for production-grade environments.

---
