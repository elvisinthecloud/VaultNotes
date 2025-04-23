
tags: #az104 #azurebastion #jumpbox #security #vmaccess #paas

---

## 🧭 Overview

Both **Azure Bastion** and a **self-hosted jump box** (bastion VM) serve the same purpose:
> Allow secure remote access (RDP or SSH) to VMs that **do not have public IPs**.

But how they achieve that is **very different**.

---

## 🔐 What Is Azure Bastion?

**Azure Bastion** is a **fully managed PaaS service** that provides **secure RDP/SSH access** to VMs **directly from the Azure Portal** — without exposing those VMs to the public internet.

### ✅ Key benefits:
- No public IP required on VMs
- Connect through **TLS (port 443)** via browser
- Managed, auto-scaled, patched by Azure
- Ideal for compliance and audit-heavy environments

---

## 🧱 What Is a Self-Hosted Jump Box?

A **jump box** (or traditional bastion host) is a **VM you manually deploy**, configure, and maintain.  
It has a public IP and acts as the **entry point** into your private network.

### 🔧 Typical tasks include:
- Manual firewall and access configuration
- Regular OS patching and monitoring
- SSH or RDP clients required on your local machine

---

## ⚔️ Side-by-Side Comparison

| Feature                              | **Azure Bastion**                     | **Self-Hosted Jump Box**            |
|--------------------------------------|----------------------------------------|-------------------------------------|
| Deployment type                      | **PaaS (Managed)**                     | **IaaS (VM you manage)**            |
| Requires public IP                   | ❌ No                                  | ✅ Yes                              |
| Browser-based access                 | ✅ Yes (Portal UI)                     | ❌ No                               |
| Ports exposed                        | Only port **443** (HTTPS)             | **22 / 3389** (SSH/RDP)             |
| Auto-scaling / patching              | ✅ Yes                                 | ❌ Manual                           |
| NSG/Firewall complexity              | Simple                                 | High                                |
| Persistent shell or tooling          | ❌ No (browser only)                  | ✅ Full control                     |
| OS/Software customization            | ❌ Not possible                        | ✅ Full flexibility                 |
| Access from outside Azure            | ✅ Yes, via Portal                     | ✅ Yes, via IP+client               |
| Cost model                           | Per-hour Bastion host pricing         | VM pricing + storage + ops         |
| Best for                             | **Security-first, compliance-ready**  | **Custom workflows, full control** |

---

## 💡 Real-World Guidance

> Use **Azure Bastion** if:
- You want **zero public IP exposure**
- You want **browser-based access** (from any device)
- You’re working in a **high-security or audited environment**
- You prefer Azure to manage patching and availability

> Use a **self-hosted jump box** if:
- You need to install **custom software/tools**
- You want **persistent shell access** or scripting tools
- You’re building something more tailored or isolated

---

## 🧠 TL;DR

| Bastion Type         | Managed? | Public IP Needed? | Use When…                              |
|----------------------|----------|--------------------|----------------------------------------|
| **Azure Bastion**    | ✅ Yes   | ❌ No              | You want security, simplicity, and compliance |
| **Jump Box (VM)**    | ❌ No    | ✅ Yes             | You want full control or customization |

---

## ✨ Personal Insight

> “In AWS, I manually built my bastion host. This is different — **Azure Bastion is a managed service** that removes the need for maintaining a jump box VM.”

That insight is 💯 on point — and shows how **Azure Bastion modernizes traditional architecture** with less overhead and more security.
