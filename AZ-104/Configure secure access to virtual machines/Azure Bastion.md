
---

## ✅ What the Question is Testing:

> To deploy Azure Bastion, what _must_ exist in the virtual network?

**Correct Answer:** `Add a new subnet`

More specifically, that subnet **must** be named:

```
AzureBastionSubnet
```

That’s a **hard Azure requirement**.

---

## 🧠 Why is this needed?

Because:

- Azure Bastion is a **fully managed jump box** (for SSH/RDP)
    
- It’s **deployed into your VNet**, but **must live in its own dedicated subnet**
    
- That subnet can’t have:
    
    - NSGs (Network Security Groups) with restrictions
        
    - Other services deployed to it
        

So you're not just **adding any subnet** — you're adding a very specific one.

---

## 🔄 Does Bastion communicate with the other subnet?

**Yes — absolutely.**

Here’s how it works:

### 🧱 Network Flow:

1. You connect to Azure Bastion **via the Azure Portal** (no public IP needed for VMs).
    
2. Azure Bastion is deployed in **its own subnet** called `AzureBastionSubnet`
    
3. From there, Bastion can **access VMs in other subnets of the same VNet** — using **private IPs**
    
4. Traffic never leaves the VNet. So it's secure and internal.
    

### 🔒 So to clarify:

|Question|Answer|
|---|---|
|Is the Bastion host in the same subnet as the target VM?|❌ No|
|Can Bastion **communicate** with other subnets in the same VNet?|✅ Yes|
|Can Bastion access **across VNets**?|✅ Only if **VNet Peering** is set up|
|Is a **service endpoint** needed?|❌ No — that’s for other Azure services (like Blob, SQL)|

---

### 🧠 Real-World Gotcha:

> **A service endpoint** is used to enable **private access to PaaS services** (like Azure SQL, Storage, etc.) from your VNet — **not for Bastion**.

This is a classic mix-up because people associate “endpoint” with “access,” but it’s a **different context**.

---

## 🧠 TL;DR:

|Feature|Needed for Bastion?|Why?|
|---|---|---|
|`AzureBastionSubnet`|✅ Yes|Dedicated subnet required for Bastion|
|Service endpoint|❌ No|Only used for PaaS services, not Bastion|
|DDoS protection|❌ Optional|Not required for Bastion to function|
|Address space|❌ Only needed if no room to add subnet||

---
