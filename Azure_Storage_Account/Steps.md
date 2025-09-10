# 🗄️ Steps to Create an Azure Storage Account

---

## 📌 Introduction
An **Azure Storage Account** provides a **unique namespace** to store and access Azure Storage services, including **Blob, File, Queue, and Table storage**.  
It is the **foundation of all Azure storage services**.

---

## 🔑 Steps to Create an Azure Storage Account

### 1️⃣ **Sign in to Azure Portal**
- Go to [Azure Portal](https://portal.azure.com).
- Log in with your Azure credentials.

---

### 2️⃣ **Create a Storage Account Resource**
- In the search bar, type **Storage Accounts**.
- Click **+ Create**.

---

### 3️⃣ **Basics Tab – Configure Core Settings**
- **Subscription** → Choose your subscription.
- **Resource Group** → Select an existing one or create a new resource group.
- **Storage Account Name** → Must be **unique**, lowercase, 3–24 characters.
- **Region** → Choose the Azure region (closest to users or data).
- **Performance**:
  - **Standard** → HDD-based, cost-effective.
  - **Premium** → SSD-based, low-latency, high-performance.
- **Redundancy** (Replication option):
  - **LRS** → Locally redundant storage.
  - **GRS** → Geo-redundant storage.
  - **ZRS** → Zone-redundant storage.
  - **RA-GRS** → Read-access geo-redundant.

---

### 4️⃣ **Advanced Tab (Optional Settings)**
- **Security**:
  - Enable **require secure transfer** (HTTPS).
  - Enable **Microsoft Defender for Storage** (threat protection).
- **Data Lake Storage Gen2** → Enable hierarchical namespace if needed for big data analytics.

---

### 5️⃣ **Networking Tab**
- Choose how the storage account can be accessed:
  - **Public endpoint (all networks)** → Open access.
  - **Selected networks** → Restrict access to specific VNets.
  - **Private endpoint** → Secure via private IP.

---

### 6️⃣ **Data Protection Tab**
- Configure **soft delete** for:
  - Blob containers
  - File shares
- Enable **point-in-time restore** for blobs (optional).

---

### 7️⃣ **Tags (Optional)**
- Add metadata tags for cost tracking and resource management.  
  Example: `Environment = Production`, `Owner = DataEngineeringTeam`.

---

### 8️⃣ **Review + Create**
- Review all configurations.
- Click **Create** to deploy the storage account.

---

### 9️⃣ **Access the Storage Account**
- Once deployment is complete:
  - Go to **Resource**.
  - Access services:
    - **Blob storage** (object storage).
    - **File shares** (SMB-based).
    - **Queues** (message storage).
    - **Tables** (NoSQL key-value store).

---

## 📊 Azure Storage Account Workflow

```
+-------------------+
|   Azure Portal    |
+---------+---------+
|
v
+-------------------+
| Storage Account   |
|  (Namespace)      |
+---------+---------+
|
+-------------------------------+
|                               |
+--------------+   +----------------+  +----------------+
| Blob Storage |   | File Storage   |  | Queue Storage  |
| (Objects)    |   | (SMB Shares)   |  | (Messaging)    |
+--------------+   +----------------+  +----------------+
|
+--------------+
| Table Storage|
| (NoSQL DB)   |
+--------------+
```

---

## 🎯 Key Takeaways
- Azure Storage Account is the **entry point** to all Azure storage services.  
- Choose **redundancy options** based on durability needs.  
- Use **Networking & Security** settings for controlled access.  
- Supports **Blob, File, Queue, and Table storage**.  

---
