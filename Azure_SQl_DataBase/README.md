## 🛢️ Azure SQL Database

**Azure SQL Database** is a fully managed **Platform as a Service (PaaS)** database engine by Microsoft that provides built-in features like high availability, backups, scalability, and security without user involvement in infrastructure management.

---

### 🚀 Key Features

| Feature                    | Description                                                                 |
|----------------------------|-----------------------------------------------------------------------------|
| ⚙️ Fully Managed           | No server maintenance, automatic patching, backups                          |
| 📈 Scalability             | Scale compute and storage independently (DTU or vCore models)               |
| 📦 Built-in Backup         | Point-in-time restore, geo-redundant backup                                 |
| 🔐 Security                | Data encryption, auditing, firewall, Azure AD authentication                |
| 📊 Intelligent Tuning      | Automatic performance tuning, query insights                                |
| 🌍 Geo-Replication         | Active geo-replication for disaster recovery                                |
| 🧪 Dev/Test Integration    | Easily integrate with Azure DevOps or GitHub Actions                        |

---

### 🏗️ Deployment Models

| Model                | Description                                    |
|----------------------|------------------------------------------------|
| **Single Database**  | Isolated DB with its own resources             |
| **Elastic Pool**     | Multiple databases sharing resources           |
| **Managed Instance** | SQL Server with near 100% compatibility        |

---

### 💵 Purchasing Models

| Model          | Key Points                       |
|----------------|----------------------------------|
| **DTU**        | Abstract compute/storage blend   |
| **vCore**      | Independent scaling, predictable |
| **Serverless** | Auto-scale compute               |
| **Hyperscale** | Supports 100TB+, fast backups    |

---

### 🛠️ Example: Create SQL Database (Azure CLI)

```bash
# Create a resource group
az group create --name myResourceGroup --location eastus

# Create a logical SQL server
az sql server create \
  --name my-sql-server \
  --resource-group myResourceGroup \
  --location eastus \
  --admin-user myadmin \
  --admin-password MyPassword123!

# Create a SQL Database
az sql db create \
  --resource-group myResourceGroup \
  --server my-sql-server \
  --name myDatabase \
  --service-objective S0
```

---

### 🔐 Security Features

- 🔐 **TDE (Transparent Data Encryption)**
- 🔐 **Firewall rules & Private Endpoints**
- 🔐 **Azure AD authentication**
- 🧾 **Auditing & Threat detection**

---

### 🔄 High Availability

Azure SQL has **built-in high availability**:
- Zone Redundant (ZRS)
- Active Geo-Replication
- Auto-failover groups (for multi-region HA)

---

### 🧠 Intelligent Features

- Query Performance Insight
- Index Advisor
- Automatic tuning (create/drop/rebuild indexes)
- Query Store

---

### 🧾 Connection String Sample

```plaintext
Server=tcp:my-sql-server.database.windows.net,1433;
Initial Catalog=myDatabase;
Persist Security Info=False;
User ID=myadmin;
Password=MyPassword123!;
MultipleActiveResultSets=False;
Encrypt=True;
TrustServerCertificate=False;
Connection Timeout=30;
```

---
