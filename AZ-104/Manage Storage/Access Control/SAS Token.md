
---
### 🔐 What is a SAS Token?

A **SAS (Shared Access Signature)** is a **secure token** that gives **time-limited, permission-scoped access** to Azure Storage resources.

The SAS token is like:

```
?sv=2023-11-03&ss=b&srt=o&sp=rl&se=2025-04-22T00:00:00Z&st=2025-04-20T12:00:00Z&spr=https&sig=abcd1234...
```

It’s **appended to the URL** of your blob, container, file, or other storage object — and users **access the object directly with this full URL**. - SEE: [[SAS User Access Scenario]]

---

### ✅ How Do You Generate a SAS Token?

You can create a SAS in **four ways**:

#### 1. **Azure Portal**

- Go to your **Blob Storage account > Containers > Your Blob or Container**
    
- Click on **"Shared access signature"**
    
- Choose:
    
    - Allowed permissions (read/list/write/delete/etc.)
        
    - Start & expiry time
        
    - Allowed IP ranges
        
    - HTTPS-only enforcement
        
- Click **Generate SAS token and URL**
    

This gives you:

- **SAS token only**
    
- **SAS URL** (full blob URL with token appended)
    

#### 2. **Azure CLI**

```bash
az storage blob generate-sas \
  --account-name mystorageacct \
  --container-name mycontainer \
  --name myfile.txt \
  --permissions r \
  --expiry 2025-04-22T00:00Z \
  --https-only \
  --ip 203.0.113.0-203.0.113.255 \
  --account-key <your-storage-account-key>
```

Then you paste the SAS into:

```bash
https://mystorageacct.blob.core.windows.net/mycontainer/myfile.txt?<sas-token>
```

#### 3. **Azure PowerShell**

```powershell
New-AzStorageBlobSASToken -Container mycontainer -Blob myfile.txt -Permission r -ExpiryTime (Get-Date).AddDays(1)
```

#### 4. **Code (C#, Python, etc.)**

Use the Azure SDK to generate SAS programmatically if you're building apps.

---

### ✉️ Do You Send This Token to Others?

**Yes** — whoever you want to grant access to, **you share the full SAS URL with them.**  
That URL **acts like a key**.

So you might email it, put it in an app, or return it as part of an API.

But be careful:

- If the SAS is **too permissive**, it could be misused.
    
- If the expiration is **too long**, it becomes a lingering security risk.
    

---

### 🧠 What Can You Use SAS With?

SAS isn’t just for blob storage — here’s where you can use it:

| Storage Type          | Can Use SAS? | Common Uses                             |
| --------------------- | ------------ | --------------------------------------- |
| **Blob Storage**      | ✅ Yes        | Files, images, backups                  |
| **File Shares (SMB)** | ✅ Yes        | Temporary file share access             |
| **Queues**            | ✅ Yes        | Messaging between apps                  |
| **Tables**            | ✅ Yes        | Structured NoSQL-style data             |
| **Containers**        | ✅ Yes        | Grant access to entire folders of blobs |

---

### 🧠 TL;DR:

|Question|Answer|
|---|---|
|What is a SAS token?|A time-limited, permission-based access token|
|How do you generate it?|Azure Portal, CLI, PowerShell, SDK|
|Do you give it to users?|✅ Yes — you share the **SAS URL**|
|Can it be used outside Blob Storage?|✅ Yes — for File Shares, Queues, Tables too|

---

Let me know if you want to practice generating SAS for different storage types or go deeper into **account-level SAS vs service-level SAS**.