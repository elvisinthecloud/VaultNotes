## 🔐 Azure Firewall Rule Collection Types – Summary

---

### ✅ 1. Application Collection Rules
- **Purpose**: Control HTTP/S traffic based on FQDNs (e.g., `*.microsoft.com`)
- **Layer**: Layer 7 (Application layer)
- **Direction**: Outbound only
- **Supports FQDNs**: ✅ Yes
- **Use Case**: Allow outbound web access to trusted domains (e.g., software update URLs, GitHub)

---

### ✅ 2. Network Collection Rules
- **Purpose**: Allow or deny traffic based on IP addresses, ports, and protocols (TCP, UDP, etc.)
- **Layer**: Layer 3/4 (Network/Transport layer)
- **Direction**: Inbound and outbound
- **Supports FQDNs**: ❌ No
- **Use Case**: Allow TCP 1433 from one subnet to another, or deny outbound port 22

---

### ✅ 3. NAT Collection Rules
- **Purpose**: Translate incoming traffic on a public IP to a private IP inside the network
- **Layer**: NAT (Port forwarding)
- **Direction**: Inbound only
- **Supports FQDNs**: ❌ No
- **Use Case**: Forward port 443 from the firewall's public IP to an internal VM's IP

---

### 🧠 Key Differentiator:
> Only **Application Collection Rules** support **FQDN-based filtering**.  
> NAT = Port forwarding, Network = IP/protocol rules, Application = Domain name rules.
