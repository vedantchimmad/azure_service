# 🗄️ Steps to Create Azure SQL Database

---

## 📌 Introduction
Azure SQL Database is a **fully managed relational database service** built on Microsoft SQL Server engine.  
It supports **scalability, high availability, security, and intelligent performance** without managing infrastructure.

---

## 🛠️ Steps to Create Azure SQL Database

### 1️⃣ **Sign in to Azure Portal**
- Go to [https://portal.azure.com](https://portal.azure.com).
- Use your **Azure account credentials**.

---

### 2️⃣ **Create a Resource**
- From the left menu, click **Create a resource**.
- Search for **SQL Database**.
- Click **Create**.

---

### 3️⃣ **Basics Tab**
Fill in the required fields:
- **Subscription** → Select your Azure subscription.
- **Resource Group** → Choose an existing or create a new resource group.
- **Database Name** → Enter the database name (e.g., `salesdb`).
- **Server** → Create a new server or use an existing one:
  - Server name (unique globally).
  - Server admin login & password.
  - Choose **Region** (e.g., East US).
- **Compute + Storage** → Choose pricing tier (vCore or DTU).

---

### 4️⃣ **Networking Tab**
- **Connectivity method** → Public endpoint or Private endpoint.
- **Firewall rules**:
  - Allow Azure services to access the server.
  - Add client IP for local connections.
- **Connection policy** → Default (recommended).

---

### 5️⃣ **Security Tab**
- Configure:
  - **Microsoft Defender for SQL** (optional).
  - **Transparent Data Encryption (TDE)** (enabled by default).
  - **Ledger** (optional for immutable storage).

---

### 6️⃣ **Additional Settings**
- **Data source**:
  - Blank database.
  - Sample database (AdventureWorksLT).
  - Restore from backup.
- **Collation** → Choose database collation (default: `SQL_Latin1_General_CP1_CI_AS`).

---

### 7️⃣ **Tags (Optional)**
- Add tags for cost tracking & organization.  
  Example:  
  - `Environment = Dev`  
  - `Project = SalesAnalytics`

---

### 8️⃣ **Review + Create**
- Review your configuration.
- Click **Create**.
- Deployment will begin → Takes a few minutes.

---

### 9️⃣ **Access the Database**
- Go to the **SQL Database resource** once deployment is complete.
- Copy **server name** (e.g., `myserver.database.windows.net`).
- Connect using:
  - **Azure Data Studio**
  - **SQL Server Management Studio (SSMS)**
  - **ADF, Databricks, Power BI**

---

## 📊 Azure SQL Database Creation Workflow

```

+-----------------+       +-------------------+       +-------------------+
|  Sign in Azure  | --->  |  Create SQL DB    | --->  | Configure Server   |
+-----------------+       +-------------------+       +-------------------+
|                          |                          |
v                          v                          v
Choose Pricing Tier       Configure Network           Add Security & TDE
|                          |                          |
v                          v                          v
Add Tags (Optional) -----> Review + Create -------> Deploy + Connect
```

---

## 🎯 Key Notes
- Choose **vCore model** for flexibility & scalability.  
- Always enable **firewall rules or private endpoint** for security.  
- Use **sample database (AdventureWorksLT)** for testing.  
- Manage with **SSMS / Azure Data Studio** for queries & administration.  

---

