
---

## 🔑 **Availability Set vs Availability Zone**

These are **two different approaches** to ensure **high availability** for your Azure virtual machines, but they operate on **different layers of Azure's infrastructure**.

---

### 🏢 **Availability Set** (Infrastructure Redundancy Within a Datacenter)

> A **logical grouping** that ensures VMs are spread across **fault domains** and **update domains** **within a single Azure datacenter**.

#### ✅ Used for:

- Ensuring high availability **within the same datacenter**
    
- Protecting VMs from **hardware failures or maintenance events**
    

#### 🔧 Key Concepts:

- **Fault Domain (FD):** Different racks, power sources, and network switches.
    
- **Update Domain (UD):** Different maintenance schedules (so not all VMs are rebooted at once).
    

#### 📈 SLA:

- **99.95%** when **2+ VMs** are in the set with managed disks
    

#### 📍 Location:

- All VMs in an Availability Set are in the **same region** and **same datacenter** (i.e., not zone-resilient)
    

#### 📦 Example Use Case:

> You’re hosting a web app on 2 VMs and want to ensure that if one physical server fails or gets updated, the other keeps running.

---

### 🌍 **Availability Zone** (Physical Datacenter-Level Redundancy)

> **Physically separate datacenters** in the **same Azure region**, each with independent power, cooling, and networking.

#### ✅ Used for:

- Ensuring **maximum fault isolation**
    
- Surviving **datacenter-wide failures**
    

#### 🔧 Key Concepts:

- Azure regions with Zones (like East US 2, West Europe) usually have **Zone 1, Zone 2, Zone 3**
    
- You place your resources **in different zones** for redundancy
    

#### 📈 SLA:

- **99.99%** when you deploy **VMs across multiple zones**
    

#### 📍 Location:

- Still in the **same region**, but **different datacenters**
    

#### 📦 Example Use Case:

> You're running mission-critical services and want to survive a **full datacenter outage**.

---

## 🧠 TL;DR Comparison Table

|Feature|**Availability Set**|**Availability Zone**|
|---|---|---|
|Type of Redundancy|Logical grouping within 1 datacenter|Physical separation across datacenters|
|Domains used|Fault Domains & Update Domains|Physical Zones (Zone 1/2/3)|
|SLA (2+ VMs)|✅ 99.95%|✅ 99.99%|
|Region scope|One datacenter in region|Multiple datacenters in region|
|Used for|High availability|High availability + fault isolation|
|Works with Managed Disks|✅ Yes|✅ Yes|

---

### 🧠 Gotcha to Remember (for AZ-104):

> **Availability Sets ≠ Zones**  
> You don’t place an Availability Set across multiple zones — they’re separate availability strategies.

---
