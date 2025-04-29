
---

## ❓ Question Breakdown

### Scenario Summary:

You have:

- A client (`getcloudskillsclient1`) connected to an Azure Virtual Network (`getcloudskillsnetwork`) via **Point-to-Site (P2S) VPN**, using a **self-signed certificate**.
    
- Now you want **another computer** (`getcloudskillsclient2`) to also connect to the **same VNet** using P2S VPN.
    
- You download the **VPN client config** and install it on client2.
    
- You **join client2 to Azure AD**.
    
- You ask: “Does joining it to Azure AD fulfill the requirement for connection?”
    

---

## 🎯 Core Concepts Being Tested

### 🔐 Point-to-Site VPN with Self-Signed Certificates

There are three **authentication options** for P2S VPNs:

1. **Azure certificate authentication (client certs)**
    
2. **Azure AD authentication**
    
3. **RADIUS authentication**
    

This scenario uses:

> ✅ **Self-signed certificate authentication**

So the **client** must have a valid client certificate **issued from the trusted root certificate** that was uploaded to the VPN gateway.

---

## 🧨 Why the Answer is ❌ No

Joining `client2` to Azure AD does **nothing** in the context of **certificate-based P2S VPN authentication**.

To connect, the client must:

- Have the **client certificate installed locally** (from the trusted root certificate that matches the VPN gateway setup)
    
- Have the **VPN client configuration installed** (usually via a `.zip` installer downloaded from the VPN Gateway)
    

> ✅ Without that certificate, even if the machine is Azure AD joined, the authentication will **fail**.

### 🔁 Key Dependency:

- **Every device using certificate-based P2S VPN must have the client certificate** (copied from the cert authority or exported from another device like client1)
    

---

## 🧠 Real-World "Gotchas"

- 🔐 **Azure AD join only matters** if you’re using **Azure AD authentication**, not certificate authentication.
    
- 📂 **Certificates aren’t magically available on all machines** — you must **export/import** them securely between devices.
    
- 🔎 If you forget to install the cert, the VPN client will install fine but **you’ll see connection errors**, typically related to auth failure.
    

---

## 🧾 Obsidian Save — Study Note Format

### 🌐 P2S VPN (Point-to-Site) - Certificate Based

#### 🔐 Client Certificate Requirements:

- Every client **must have the client certificate** installed.
    
- Certificate must be issued from the **root cert uploaded to the Azure VPN Gateway**.
    

#### ❌ Joining a device to Azure AD does **not** enable VPN connectivity for cert-based auth.

#### ✅ Azure AD Join is **only required** if you use **Azure AD-based P2S authentication**.

---

### 📌 AZ-104 Exam Objective:

> **Configure and manage virtual networks** → _Configure Point-to-Site VPNs (certificate-based, Azure AD-based, RADIUS-based)_

---

## ✅ Summary Answer

|Question|Answer|
|---|---|
|Does Azure AD join satisfy the requirement for P2S VPN with cert-based auth?|❌ **No**|
|What is required instead?|✅ **Install the client certificate on the new machine** (client2)|
|What would Azure AD help with?|Only in **Azure AD-based P2S VPN**, **not** cert-based|

---

Let me know if you'd like a **PowerShell example** or GUI walk-through on how to **export/import client certs** between machines for this setup — that’s a useful real-world skill to have.