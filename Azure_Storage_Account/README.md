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
## 💾 Azure Storage Terminology

Azure Storage is a Microsoft cloud storage solution designed for durability, scalability, and high availability. It supports structured, semi-structured, and unstructured data across multiple storage types.

---

### 📦 Core Terms in Azure Storage

#### 1. ☁️ **Storage Account**

- A **storage account** provides a unique namespace in Azure for your data.
- It is a top-level container that holds all storage services (Blob, File, Table, Queue).

```bash
Example: mystorageaccount.blob.core.windows.net
```

---

#### 2. 🪣 **Container**

- A **container** organizes blobs (like a folder).
- Required for storing blobs in Azure Blob Storage.

```bash
Container: mycontainer → Blobs: image1.jpg, data.csv
```

---

#### 3. 📁 **Blob (Binary Large Object)**

- Used to store **unstructured data** (e.g., images, videos, backups).
- Blob types:
    - **Block Blob**: Ideal for storing text and binary files.
    - **Append Blob**: For log files that grow over time.
    - **Page Blob**: Optimized for frequent read/write, used for VHDs.

---

#### 4. 🗃️ **File Share (Azure Files)**

- Fully managed file share accessible via **SMB or NFS protocols**.
- Use case: Lift-and-shift file server replacement.

---

#### 5. 📨 **Queue Storage**

- Message-based communication between application components.
- Supports **asynchronous messaging**.

```bash
Queue: taskqueue → Messages: [“Job1”, “Job2”]
```

---

#### 6. 🧾 **Table Storage**

- A NoSQL key-value store for structured, non-relational data.
- Highly scalable with low latency.

---

### 🧱 Storage Tiers

| Tier         | Description                      | Use Case                          |
|--------------|----------------------------------|------------------------------------|
| Hot          | High access frequency            | Frequently accessed data           |
| Cool         | Infrequent access, lower cost    | Backup and archival with some access |
| Archive      | Rare access, lowest cost         | Long-term retention (cold data)    |

---

### 🔐 Access Control & Security

- **Shared Access Signature (SAS)**: Temporary URL with scoped permissions.
- **Access Keys**: Keys used to authenticate the storage account.
- **Private/Public Access**: Control who can read container blobs.

---

### 📊 Redundancy Options (Replication)

| Redundancy Type   | Description                                       |
|-------------------|---------------------------------------------------|
| LRS               | Locally Redundant Storage (within a single DC)    |
| ZRS               | Zone-Redundant Storage (across AZs)               |
| GRS               | Geo-Redundant Storage (paired region backup)      |
| RA-GRS            | Read-Access GRS (readable geo backup)             |

---

### 📍 Endpoints

Each storage type has a unique endpoint:

```text
Blob:    https://<account>.blob.core.windows.net/
File:    https://<account>.file.core.windows.net/
Queue:   https://<account>.queue.core.windows.net/
Table:   https://<account>.table.core.windows.net/
```

---

### 🧰 Tools to Access Storage

- **Azure Portal**
- **Azure Storage Explorer**
- **Azure CLI & PowerShell**
- **REST API / SDKs**

---
