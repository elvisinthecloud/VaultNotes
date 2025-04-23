
tags: #az104 #vmss #sla #availability #highavailability #manage-vms

> This is a classic AZ-104 trap question. The confusion around scale sets vs availability sets often comes down to what Azure **guarantees in writing** for SLAs.

---

## 🧾 Scenario Recap

You’re asked to deploy:
- **Two Azure VMs**
- Using **managed disks**
- And meet a **99.95% SLA**

You propose a **Virtual Machine Scale Set** (VMSS) solution.

---

## ❌ Why a Scale Set *Alone* Doesn’t Meet SLA

> **VM Scale Sets** only meet the **99.95% SLA** if they use **Availability Zones**.

By default:
- ✅ VMSS distributes VMs across fault and update domains.
- ❌ It does **not guarantee redundancy across zones**.
- ❌ So, it does **not qualify** for the 99.95% SLA.

### 🚨 Microsoft’s official SLA states:
> You must deploy **2 or more VMs in an Availability Set** or **across Availability Zones** to meet the 99.95% SLA.

---

## ⚖️ Key Comparison

| Deployment Type                          | SLA Met? | Notes |
|------------------------------------------|----------|-------|
| 2 VMs in **Availability Set**            | ✅ 99.95% | Valid under SLA rules |
| 2 VMs in **Scale Set** (default config)  | ❌        | No zone redundancy |
| 2 VMs in **Scale Set with Zones enabled**| ✅ 99.99% | But **must be explicitly zonal** |

---

## 💡 Clarification

You were right to think:
> “2 VMs with managed disks = 99.95% SLA”

**BUT** the question:
- Used a **Scale Set**, not an Availability Set
- Didn’t mention **zones**
- Therefore: ❌ **Not compliant with the SLA requirements**

---

## ✅ What *Would* Meet the SLA?

- **Correct**: 2+ VMs with managed disks in an **Availability Set**
- **Correct**: 2+ VMs in a **Scale Set with Zone Balancing**
- **Incorrect**: Scale Set (default config) with no mention of zones

---

## 🧠 TL;DR

| Setup                                          | SLA | SLA Met? | Reason |
|------------------------------------------------|-----|----------|--------|
| 2 VMs + Managed Disks + Availability Set       | 99.95% | ✅ | Azure guarantees this config |
| 2 VMs + Managed Disks + Scale Set (default)    | N/A    | ❌ | Doesn’t guarantee zone separation |
| 2 VMs + Managed Disks + Scale Set w/ Zones     | 99.99% | ✅ | Must be explicitly zonal |

---

### ✅ Key Takeaway

> **You don’t get an SLA just because you scale** — you get it by deploying across failure boundaries Azure recognizes in their SLA.

