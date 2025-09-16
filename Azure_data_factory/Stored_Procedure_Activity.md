# 📝 Stored Procedure Activity in Azure Data Factory (ADF)

---

## 📌 Introduction
The **Stored Procedure Activity** in ADF allows you to **invoke stored procedures in Azure SQL Database, Synapse Analytics, or SQL Server** from a pipeline.  
It is typically used for **data transformations, aggregations, or applying business logic** within the database layer.

---

## ⚙️ Key Features
- Executes **stored procedures** as part of data workflows.  
- Supports **input, output, and return parameters**.  
- Can pass **dynamic pipeline parameters/variables** as stored procedure parameters.  
- Works with **linked services** like Azure SQL DB, Synapse, or SQL Server.  

---

## 🛠️ Properties

| Property             | Description |
|----------------------|-------------|
| **Name**             | Activity name. |
| **Linked Service**   | Connection to Azure SQL Database, Synapse, or SQL Server. |
| **Stored Procedure Name** | The procedure to call. |
| **Stored Procedure Parameters** | Name-value pairs to pass into the stored procedure. |

---

## 📊 Example 1: Execute Stored Procedure Without Parameters
```json
{
  "name": "RunStoredProcedure",
  "type": "SqlServerStoredProcedure",
  "typeProperties": {
    "storedProcedureName": "usp_UpdateSalesSummary"
  },
  "linkedServiceName": {
    "referenceName": "AzureSqlDatabase_LinkedService",
    "type": "LinkedServiceReference"
  }
}
````

➡️ Executes `usp_UpdateSalesSummary` stored procedure.

---

## 📊 Example 2: Stored Procedure With Parameters

```json
{
  "name": "RunStoredProcedureWithParams",
  "type": "SqlServerStoredProcedure",
  "typeProperties": {
    "storedProcedureName": "usp_LoadSalesData",
    "storedProcedureParameters": {
      "StartDate": { "value": "2025-09-01", "type": "String" },
      "EndDate": { "value": "@pipeline().parameters.ProcessDate", "type": "String" }
    }
  },
  "linkedServiceName": {
    "referenceName": "AzureSqlDatabase_LinkedService",
    "type": "LinkedServiceReference"
  }
}
```

➡️ Passes parameters `StartDate` and `EndDate` into the procedure.

---

## 📊 Example 3: Using Output Parameters

Stored Procedure definition:

```sql
CREATE PROCEDURE usp_GetRecordCount
    @TableName NVARCHAR(100),
    @RowCount INT OUTPUT
AS
BEGIN
    DECLARE @sql NVARCHAR(MAX)
    SET @sql = 'SELECT @RowCount = COUNT(*) FROM ' + @TableName
    EXEC sp_executesql @sql, N'@RowCount INT OUTPUT', @RowCount OUTPUT
END
```

ADF Activity:

```json
{
  "name": "RunStoredProcedureWithOutput",
  "type": "SqlServerStoredProcedure",
  "typeProperties": {
    "storedProcedureName": "usp_GetRecordCount",
    "storedProcedureParameters": {
      "TableName": { "value": "Sales", "type": "String" },
      "RowCount": { "value": "0", "type": "Int", "direction": "Output" }
    }
  },
  "linkedServiceName": {
    "referenceName": "AzureSqlDatabase_LinkedService",
    "type": "LinkedServiceReference"
  }
}
```

➡️ Output parameter `RowCount` will be captured in activity output.

---

## 🚀 Workflow Example

**Scenario:** Load sales data into staging, then run a stored procedure to update summary tables.

Pipeline steps:

1. **Copy Activity** → Load data into `Sales_Staging`.
2. **Stored Procedure Activity** → Call `usp_UpdateSalesSummary` to refresh summary tables.

---

## 🎯 Best Practices

* Use stored procedures for **complex transformations** to reduce ADF overhead.
* Pass **pipeline parameters** to stored procedures for dynamic execution.
* Always handle **output parameters** carefully if used for downstream activities.
* Use **integration runtime** correctly (Azure IR or Self-hosted IR).

---

## 🏆 Key Takeaways

* **Stored Procedure Activity** integrates ADF with SQL-based processing.
* Supports **input, output, and return parameters**.
* Ideal for **business logic, aggregations, and batch processing**.
* Enhances performance by pushing work to the **database engine**.

---
