# 🔗 Linked Service Parameterization in Azure Data Factory (ADF)

---

## 📌 Introduction
**Linked Service Parameterization** in ADF allows you to create **dynamic and reusable linked services** by defining parameters that can change at runtime.  

Instead of hardcoding values like:
- Server name  
- Database name  
- Account name  
- File system name  

➡️ You can define them as **parameters**, making pipelines flexible across **Dev, Test, and Prod environments**.

---

## ⚙️ Why Use Linked Service Parameterization?
- Avoids **hardcoding** connection details.  
- Supports **multi-environment deployments**.  
- Allows **dynamic runtime connections**.  
- Works with **datasets and activities** seamlessly.  

---

## 🛠️ Steps for Linked Service Parameterization

### 1️⃣ Define Parameters in Linked Service
Example: Azure SQL Database Linked Service  
```json
{
  "name": "AzureSqlDatabaseLS",
  "type": "Microsoft.DataFactory/factories/linkedservices",
  "properties": {
    "parameters": {
      "DBName": { "type": "String" },
      "ServerName": { "type": "String" }
    },
    "type": "AzureSqlDatabase",
    "typeProperties": {
      "connectionString": "Server=tcp:@{linkedService().ServerName}.database.windows.net;Database=@{linkedService().DBName};"
    }
  }
}
````

---

### 2️⃣ Reference Linked Service Parameters in Datasets

```json
{
  "name": "SqlDataset",
  "properties": {
    "linkedServiceName": {
      "referenceName": "AzureSqlDatabaseLS",
      "type": "LinkedServiceReference",
      "parameters": {
        "ServerName": "myserver-dev",
        "DBName": "SalesDB"
      }
    },
    "type": "AzureSqlTable",
    "typeProperties": {
      "tableName": "SalesData"
    }
  }
}
```

---

### 3️⃣ Pass Values at Runtime from Pipeline

You can override linked service parameters dynamically from **pipeline parameters**.

```json
{
  "name": "CopyPipeline",
  "properties": {
    "parameters": {
      "EnvServer": { "type": "String" },
      "EnvDB": { "type": "String" }
    },
    "activities": [
      {
        "name": "CopyActivity",
        "type": "Copy",
        "inputs": [
          {
            "referenceName": "SqlDataset",
            "type": "DatasetReference",
            "parameters": {
              "ServerName": "@pipeline().parameters.EnvServer",
              "DBName": "@pipeline().parameters.EnvDB"
            }
          }
        ]
      }
    ]
  }
}
```

---

## 🔑 Example Use Cases

1. **Dev/Test/Prod Switching**

    * Server: `dev-sql.database.windows.net`
    * Server: `prod-sql.database.windows.net`
    * Pass environment-specific values via parameters.

2. **Dynamic Database Connections**

    * Single Linked Service can connect to multiple databases (`SalesDB`, `HRDB`, `FinanceDB`).

3. **Reusable Pipelines**

    * Avoid creating multiple linked services for different environments.

---

## 📊 Example Workflow

**Pipeline Goal:** Load files into different SQL Databases for each environment.

1. **Pipeline Parameters:** `EnvServer`, `EnvDB`.
2. **Linked Service Parameters:** `ServerName`, `DBName`.
3. **Dataset:** Pass values from pipeline → linked service.
4. **Copy Activity:** Runs dynamically based on environment.

Diagram:

```
Pipeline Params (EnvServer, EnvDB)
        ↓
Dataset (Pass to LS Params)
        ↓
Linked Service (Dynamic Connection)
        ↓
Copy Activity
```

---

## 🎯 Best Practices

* Always parameterize **ServerName, DatabaseName, AccountName**.
* Use **Azure Key Vault** for credentials (do not parameterize passwords directly).
* Use **global pipeline parameters** for environment management.
* Keep default values for debugging in development.

---

## 🏆 Key Takeaways

* **Linked Service Parameterization** makes connections **dynamic and reusable**.
* Reduces duplication when working across **Dev, Test, and Prod**.
* Works seamlessly with **pipeline + dataset parameterization**.
* Best practice: **Combine with Key Vault and Managed Identity** for secure credentials.

---