


---
# Deploying ARM Templates via Azure CLI
tags: #az104 #armtemplates #cli #automation #compute #iac

---

## 🧾 Overview

**ARM (Azure Resource Manager) templates** are JSON files used to define Azure infrastructure as code (IaC).  
You can deploy them using Azure CLI with or without an accompanying parameters file — no scripts required.

---

## 📁 Required Files

| File | Required? | Purpose |
|------|-----------|---------|
| `azuredeploy.json` | ✅ Yes | The main ARM template |
| `azuredeploy.parameters.json` | 🔁 Optional | Input values for the template parameters |
| `.ps1` or `.sh` script files | ❌ No | Only needed if you’re scripting automation around the deployment |

> ✅ The template file is the only required file.  
> 🔁 Parameter file is used when input values are defined as parameters in the template.

---

## 📦 Example Folder Structure



---

## 🧪 Sample ARM Template (azuredeploy.json)

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2019-04-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "storageAccountName": { "type": "string" },
    "location": { "type": "string", "defaultValue": "eastus" }
  },
  "resources": [
    {
      "type": "Microsoft.Storage/storageAccounts",
      "apiVersion": "2022-09-01",
      "name": "[parameters('storageAccountName')]",
      "location": "[parameters('location')]",
      "sku": { "name": "Standard_LRS" },
      "kind": "StorageV2",
      "properties": {}
    }
  ]
}
```

---

## 🔧 Sample Parameter File (azuredeploy.parameters.json)

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2019-04-01/deploymentParameters.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "storageAccountName": { "value": "mystoragefromcli01" },
    "location": { "value": "eastus" }
  }
}
```

---

## 🚀 Deployment Command (Azure CLI)

### ✅ With parameter file:

```bash
az deployment group create \
  --resource-group MyResourceGroup \
  --template-file azuredeploy.json \
  --parameters @azuredeploy.parameters.json
```

### ✅ Without parameter file (inline):

```bash
az deployment group create \
  --resource-group MyResourceGroup \
  --template-file azuredeploy.json \
  --parameters storageAccountName=mystorage01 location=eastus
```

---

## 🧠 TL;DR

- **Required**: ARM template file (`azuredeploy.json`)
    
- **Optional**: Parameters file (`azuredeploy.parameters.json`)
    
- **Not needed**: `.ps1` or `.sh` script (unless part of automation)
    

You can run ARM templates _directly_ via Azure CLI — no wrapper script is required.

---

> 💡 Pro Tip: Use parameter files for reusability across dev, staging, and prod environments.
