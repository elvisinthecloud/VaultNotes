

---

### ✅ What is **Soft Delete** in Azure Blob Storage?

Soft Delete is like Azure’s **“undo button”** for blob deletions.

#### 🎯 Main purpose:

> Protect blob data from **accidental deletion or overwrite** for a set retention period — like **14 days** in your question.

---

### 🔍 How it Works:

- A user (or app) **deletes a blob**.
    
- Instead of being immediately removed from Azure, the blob is marked as **soft deleted**.
    
- It becomes **invisible to normal listing and reading**, but **still recoverable**.
    
- You can restore the blob within the configured retention period (e.g., 14 days).
    
- After that, it's permanently deleted.
    

📌 Think of it like:

```
User: “Oops, I deleted a blob 😬”
Azure: “No worries, I saved it in the recycle bin for 14 days 💾”
```

---

### 🔧 Where You Configure It:

In the **Storage Account > Data Protection** section (or CLI), you enable:

```bash
--enable-delete-retention true
--delete-retention-days 14
```


---

### 🧠 TL;DR:

|Feature|Purpose|Example|
|---|---|---|
|**Soft Delete**|Recover deleted blobs|"I deleted a file yesterday — restore it!"|
|**Lifecycle Management**|Automate blob movement/deletion|"Move files older than 30 days to Cool tier"|

---

