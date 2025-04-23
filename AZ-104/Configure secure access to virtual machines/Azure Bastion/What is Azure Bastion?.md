# Azure Bastion: What It Is, How It Works, and Subnet Requirements
tags: #az104 #azurebastion #vmaccess #secureaccess #networking

---

## 🔐 What Is Azure Bastion?

**Azure Bastion** is a **fully managed platform-as-a-service (PaaS)** that allows you to securely connect to your **virtual machines (VMs)** using **RDP or SSH** — directly from the Azure Portal.  
This removes the need to expose **public IP addresses** on your VMs, dramatically reducing the attack surface.

---

### ✅ Key Features
- Access VMs securely over **TLS/HTTPS (port 443)** — no open RDP/SSH ports needed
- Protects against **port scanning**, brute-force, and malware bots
- Managed by Microsoft — no need to maintain your own jump box
- Works across subnets, VNets, and even via VNet peering

---

## 🌐 Real-World Use Cases

- **Enterprise Jump Box Replacement:** Instead of hosting a VM with public RDP access, deploy Bastion for browser-based access.
- **Security-First Environments:** For environments that block all inbound traffic except HTTPS, Bastion is a go-to solution.
- **Compliance-Driven Organizations:** Bastion helps meet security and auditing requirements by keeping VMs internal-only.

---

## ✅ AZ-104 Exam Objective

> **Configure secure access to virtual machines (10–15%)**

This includes:
- Configuring **Azure Bastion**
- Just-in-Time (JIT) VM access
- NSG rules for VM protection
- Secure RDP/SSH access methods

Azure Bastion falls squarely within the **Secure VM Access** objective. It’s not just about networking — it’s about reducing exposure and hardening entry points to your VMs.

---

