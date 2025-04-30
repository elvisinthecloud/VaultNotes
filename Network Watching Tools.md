## 🛰️ Azure Network Watcher Features – What They Do & When to Use Each

> **Scenario in the quiz**  
> “Find out if there is **outbound connectivity between an Azure VM and an external host**.”  
> **Best tool:** **Connection Monitor** ✔️

Below is a concise “cheat sheet” you can paste straight into your Obsidian vault.  
It shows _what each feature does, when to pick it, and why you’d choose it over the others._

---

### 1. **Connection Monitor** (Chosen answer)

|Aspect|Details|
|---|---|
|**Purpose**|_End-to-end_ reachability & performance checks (ICMP, TCP, HTTP, HTTPS). Continuous or on-demand.|
|**Typical Question**|“Can my VM reach **this FQDN/IP** on port 443, and what’s the latency / packet loss?”|
|**Scope**|Source can be a VM, VMSS, AKS node, or on-prem machine (via Log Analytics agent). Destination can be any IP/FQDN (internal or external).|
|**Output**|Pass/Fail (reachability), RTT, hop latency, packet loss. Optional alerts.|
|**When to use**|- Verify outbound or inbound connectivity **over time**.- Monitor SLAs to SaaS endpoints (e.g., `api.github.com`).- Troubleshoot intermittent drops rather than one-off tests.|

---

### 2. **IP Flow Verify**

|Aspect|Details|
|---|---|
|**Purpose**|Simulate a _single_ TCP/UDP flow and see which NSG or Azure Firewall rule allows/denies it.|
|**Typical Question**|“Why can’t my VM talk to 10.0.2.4 on port 1433 right now?”|
|**Scope**|Works only for traffic **to/from a specific VM NIC** within the same VNet/peered VNets.|
|**Output**|**Allow / Deny**, plus the name of the rule and security group that made the decision.|
|**When to use**|- Quick NSG rule debugging.- One-shot checks (not continuous).- You already suspect a firewall/NSG issue.|
|**Why not here**|It tests a _single hop_ (NSG) — it doesn’t tell you if the packet makes it all the way to an **external host** across the internet.|

---

### 3. **Next Hop**

|Aspect|Details|
|---|---|
|**Purpose**|Determine the _routing decision_ Azure will make for a packet leaving a VM NIC (which hop / gateway is used).|
|**Typical Question**|“Will traffic from this VM to 172.16.0.5 go via the on-prem VPN gateway, the internet, or stay in Azure?”|
|**Scope**|Works per-NIC, per-destination IP.|
|**Output**|Name/type/IP of the next hop device (Internet, VNet peering, Virtual Appliance, VNet Gateway, etc.).|
|**When to use**|- Diagnose UDR mistakes.- Verify forced-tunnelling or custom route intent.- Check if traffic goes out to internet vs. through NVA.|
|**Why not here**|It only shows routing _destination_, not whether the destination responds or if ports are open.|

---

### 4. **Traffic Analytics**

|Aspect|Details|
|---|---|
|**Purpose**|**Aggregated, historical** flow-log analysis for security & usage insights (top talkers, threats, etc.).|
|**Data Source**|NSG flow logs in a Log Analytics workspace, visualised in Azure Network Watcher 📊|
|**Typical Question**|“Which IPs generate the most inbound traffic this month?”|
|**Output**|Dashboards: bytes, flows, threat IDs, geo heat-maps.|
|**When to use**|- Capacity planning.- Detecting anomalies / malicious IPs.- Compliance reporting.|
|**Why not here**|It’s **retrospective & statistical**; not a real-time connectivity test between a VM and a specific endpoint.|

---

## 👩‍🏫 Quick Decision Matrix

|Need|Best Tool|
|---|---|
|Ongoing reachability & latency to any IP/FQDN|**Connection Monitor**|
|One-off “is this port allowed/blocked” test|**IP Flow Verify**|
|Find which route/gateway a packet will take|**Next Hop**|
|Historical traffic patterns & threat insights|**Traffic Analytics**|

---

### ✏️ Copy-friendly Obsidian snippet

```markdown
### 🔎 Azure Network Watcher – Choosing the Right Tool

- **Connection Monitor** – Continuous or on-demand tests to external or internal endpoints (ICMP/TCP/HTTP). Best for verifying **outbound connectivity** over time.
- **IP Flow Verify** – Instant check if a single TCP/UDP flow is **allowed or denied** by NSG/Azure Firewall.
- **Next Hop** – Shows the **routing path** (internet, VPN, NVA, etc.) a packet from a VM will take.
- **Traffic Analytics** – Aggregated **flow-log analytics** for trends, top talkers, and threat detection (not real-time testing).
```

Feel free to let me know if you’d like hands-on examples (CLI or Portal) for any of these tools!