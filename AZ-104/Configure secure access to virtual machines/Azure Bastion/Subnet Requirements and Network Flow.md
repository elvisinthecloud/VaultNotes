

---

## 📎 Summary of Required Setup

To deploy Azure Bastion, you must:
- **Add a dedicated subnet** named: `AzureBastionSubnet`
- Use a **/27 or larger subnet mask**
- Deploy the Bastion resource **into that subnet**
- Ensure the subnet has **no conflicting NSGs or other services**
- No service endpoint or DDoS is required

---

## 🔄 Network Flow Overview

1. User logs into the **Azure Portal**
2. Opens RDP/SSH **via Bastion**
3. Bastion lives in `AzureBastionSubnet` and **privately connects** to VMs in other subnets
4. Bastion uses internal VNet routing — **no public IPs needed** on VMs

---

## 🧠 TL;DR

| Requirement                        | Required for Bastion? | Notes |
|------------------------------------|------------------------|-------|
| Dedicated Subnet (`AzureBastionSubnet`) | ✅ Yes                | Must exist before deployment |
| New address space                  | ❌ No                  | Only needed if subnet space is exhausted |
| Service endpoint                   | ❌ No                  | Not needed — used for Azure PaaS services |
| DDoS Protection                    | ❌ Optional            | Not a deployment requirement |
| NSG configuration                  | ⚠️ Avoid restrictive NSGs on Bastion subnet |

---

> Bastion = Seamless secure access to internal VMs without public IPs.  
> Exam wants to know: **what do you need in your VNet to deploy it successfully?** Answer: A subnet — not a service endpoint.
