## 🌐 Azure Global VNet Peering — Deep-Dive Summary (AZ-104 Focused)

### 🔹 What It Is:
Global VNet Peering allows **virtual networks in different Azure regions** (e.g., East US ↔ Japan East) to communicate **over private IP addresses**, using the **Microsoft backbone network**. It's low-latency, encrypted, and bypasses the public internet.

---

### ✅ Key Features:

| Feature | Supported? | Notes |
|--------|------------|-------|
| Cross-region private connectivity | ✅ Yes | This is what makes it “global” peering. |
| VM-to-VM traffic | ✅ Yes | Core use case. |
| VM-to-private data source (e.g., Azure SQL, Storage) | ✅ Yes | As long as the resource is in a **peered VNet** and uses a **private IP**. |
| Public endpoint required? | ❌ No | Works **without** exposing any public IPs. |
| Uses Azure’s private backbone? | ✅ Yes | No internet traversal. |
| DNS resolution supported? | ✅ Yes | If using Azure DNS or custom DNS properly configured. |

---

### 💡 Clarifications Based on Our Discussion:

- You originally assumed Global Peering only works **VM-to-VM**, but it also works **VM-to-private service**, like:
  - A **private Azure SQL instance**
  - A **Storage Account behind a private endpoint**
  - Any resource in a **subnet within a peered VNet**

- The scenario where an East US VM needs to access a **data source in Japan** (with no public IP) is **exactly what Global VNet Peering is for.**

---

### ❌ What *not* to use in this case:

- **Point-to-Site (P2S) VPN** from a VM:
  - 🔴 Not supported: VMs can't reliably auto-initiate VPN clients
  - 🔴 P2S is for **user devices**, not Azure infrastructure

- **VNet-to-VNet VPN gateways**:
  - 🔶 Technically valid but adds unnecessary **cost and complexity**
  - 🔶 Requires two gateways and IPsec tunnel management
  - 🔶 **Slower** and less efficient than backbone routing

---

### 🔐 Security + Routing

- Traffic remains **private** and is **encrypted in transit** via Microsoft’s backbone.
- **Network Security Groups (NSGs)** still apply — be sure to open appropriate ports across peered VNets.
- **No transitive peering** — if VNet A peers to B and B peers to C, A and C do **not** see each other unless explicitly peered.

---

### 🔗 AZ-104 Exam Objective Reference:
> **Implement and manage virtual networking** → *Configure virtual network peering (regional and global)*  
> Focus on choosing peering vs VPN vs ExpressRoute based on:
> - Scenario scope (intra-Azure vs hybrid)
> - Security
> - Latency
> - Simplicity

---

### ✅ TL;DR - When to Use Global VNet Peering:
- You need to connect **VNets across different regions**
- You need **private, encrypted communication**
- You want to avoid **VPN complexity**
- The resource has **no public endpoint**
