# 📜 Script Activity in Azure Data Factory (ADF) / Synapse

---

## 📌 Introduction
The **Script Activity** in Azure Data Factory (ADF) and Synapse is used to **run SQL scripts** on supported data stores such as **Azure SQL Database, Synapse Analytics, Snowflake, etc.**.  
It is similar to **Stored Procedure Activity**, but instead of calling a pre-defined procedure, it lets you **write inline SQL queries**.

---

## ⚙️ Key Features
- Supports **inline SQL script execution**.  
- Can run **DDL (CREATE, ALTER, DROP)** and **DML (SELECT, INSERT, UPDATE, DELETE)** statements.  
- Allows execution against multiple **linked services** (Azure SQL DB, Synapse, Snowflake, PostgreSQL, etc.).  
- Can capture **query outputs** for downstream use.  
- Supports **parameterization** for dynamic SQL execution.  

---

## 🛠️ Properties

| Property         | Description |
|------------------|-------------|
| **Name**         | Activity name. |
| **Type**         | Must be `"Script"`. |
| **Linked Service** | Connection to the target database. |
| **Script**       | SQL script or query to execute. |
| **Parameters**   | Dynamic parameters passed into the query. |
| **Output**       | Stores query result if SELECT is used. |

---

## 📊 Example 1: Simple SELECT Script
```json
{
  "name": "RunSelectScript",
  "type": "Script",
  "typeProperties": {
    "script": "SELECT COUNT(*) AS TotalRows FROM SalesData"
  },
  "linkedServiceName": {
    "referenceName": "AzureSqlDatabaseLS",
    "type": "LinkedServiceReference"
  }
}
````

➡️ Executes a query to **count rows** in the `SalesData` table.

---

## 📊 Example 2: DDL Statement (Create Table)

```json
{
  "name": "CreateTableScript",
  "type": "Script",
  "typeProperties": {
    "script": "CREATE TABLE StagingData (Id INT, Name NVARCHAR(100), CreatedDate DATETIME)"
  },
  "linkedServiceName": {
    "referenceName": "AzureSqlDatabaseLS",
    "type": "LinkedServiceReference"
  }
}
```

➡️ Creates a new table named **StagingData**.

---

## 📊 Example 3: Parameterized Script

```json
{
  "name": "ParameterizedScript",
  "type": "Script",
  "typeProperties": {
    "script": "INSERT INTO SalesLog (FileName, LoadDate) VALUES ('@{pipeline().parameters.FileName}', GETDATE())"
  },
  "linkedServiceName": {
    "referenceName": "AzureSqlDatabaseLS",
    "type": "LinkedServiceReference"
  }
}
```

➡️ Dynamically inserts pipeline parameter `FileName` into the database log table.

---

## 📊 Example 4: Capture Output from Script

```json
{
  "name": "RowCountScript",
  "type": "Script",
  "typeProperties": {
    "script": "SELECT COUNT(*) AS RowCount FROM Customers"
  },
  "linkedServiceName": {
    "referenceName": "AzureSqlDatabaseLS",
    "type": "LinkedServiceReference"
  }
}
```

➡️ Output of this script (`RowCount`) can be passed to a **Set Variable Activity** or **If Condition Activity**.

---

## 🚀 Workflow Example

**Scenario:** Validate row count before loading data.

1. **Copy Activity** → Load CSV into staging.
2. **Script Activity** → Run SQL `SELECT COUNT(*)`.
3. **If Condition** → If row count > 0, proceed to next load.
4. **Fail Activity** → Stop pipeline if no data is found.

Diagram:

```
Copy Data → Script Activity (Row Count) → If Condition → Next Step / Fail
```

---

## 🎯 Best Practices

* Use **Script Activity** for **ad-hoc SQL** instead of modifying stored procedures.
* Keep scripts **idempotent** (safe to run multiple times).
* Avoid writing overly **complex scripts** in activity; store them in DB as SPROC if reusable.
* Capture outputs for **validation and conditional branching**.

---

## 🏆 Key Takeaways

* **Script Activity** runs **inline SQL queries** within pipelines.
* Supports **DDL/DML operations** across multiple databases.
* Can be **parameterized** and **return outputs**.
* Great for **lightweight SQL logic** inside pipelines.

---
