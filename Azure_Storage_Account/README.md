## ☁️ Azure Storage Account

An **Azure Storage Account** provides a unique namespace to store and access Azure Storage data objects. It supports multiple services and is the foundation for storing files, blobs, queues, tables, and disks.

---

### 📦 Storage Services

| Service           | Description                                        | Use Case                              |
|-------------------|----------------------------------------------------|---------------------------------------|
| **Blob Storage**  | Stores unstructured data like images, documents    | Big Data, backups, media              |
| **File Storage**  | Managed file shares (SMB protocol)                 | Lift-and-shift apps, file sharing     |
| **Queue Storage** | Messaging store for reliable communication         | Decoupled architecture, microservices |
| **Table Storage** | NoSQL key-value database                           | Scalable apps with flexible schema    |
| **Disk Storage**  | Managed disks for Azure VMs                        | Persistent storage for VMs            |

---

### 🧱 Storage Account Types

| Type                      | Description                                      |
|---------------------------|--------------------------------------------------|
| **General-purpose v2**    | Recommended. Supports all storage features       |
| **General-purpose v1**    | Legacy. Lower cost, fewer features               |
| **Blob Storage**          | Optimized for blob-only access                   |
| **BlockBlobStorage**      | Premium performance for block blobs              |
| **FileStorage**           | Premium performance file shares                  |

---

### 🛠️ Key Features

- 🔐 **Encryption at rest** with Microsoft or customer-managed keys
- 🌍 **Geo-redundancy** (LRS, GRS, RA-GRS, ZRS)
- 📜 **Soft delete** for blob and file recovery
- ⏱️ **Lifecycle management** for auto-tiering
- 🔄 **Data replication** across regions
- 📊 **Metrics & monitoring** through Azure Monitor

---

### 🌐 Access Tiers (For Blob Storage)

| **Tier**    | Use Case                         |
|-------------|----------------------------------|
| **Hot**     | Frequent access                  |
| **Cool**    | Infrequent access, lower cost    |
| **Archive** | Rare access, cold storage        |

---

### 🔑 Authentication Options

- **Shared Key** (Storage Account Key)
- **Azure AD** (RBAC permissions)
- **Shared Access Signature (SAS)** – temporary delegated access

---

### 🧪 Example: ARM Template for a Storage Account

```json
{
  "type": "Microsoft.Storage/storageAccounts",
  "apiVersion": "2022-09-01",
  "name": "mystorageaccount123",
  "location": "eastus",
  "sku": {
    "name": "Standard_LRS"
  },
  "kind": "StorageV2",
  "properties": {}
}
```

---
