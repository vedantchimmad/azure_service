# 📝 Lookup Activity in Azure Data Factory (ADF)

---

## 📌 Introduction
The **Lookup Activity** in ADF is used to **retrieve data from a data source**.  
It can return a **single row** or **an entire dataset** and is often used to **fetch configuration values, control pipeline execution, or provide input to other activities**.

---

## ⚙️ Key Features
- Can query **files, tables, or queries**.  
- Returns data in **JSON format**.  
- Supports **parameterization** for dynamic lookups.  
- Useful with **Set Variable, If, ForEach, and Stored Procedure activities**.  

---

## 🛠️ Properties

| Property          | Description |
|-------------------|-------------|
| **Source Dataset** | Defines the data source (SQL, Blob, ADLS, etc.). |
| **Source Type**    | Can be **Table**, **Query**, or **File**. |
| **First Row Only** | If `true`, returns a single row (object). If `false`, returns an array of rows. |

---

## 📊 Example 1: Lookup Single Row (First Row Only = true)
Dataset: Azure SQL Table (`ConfigTable`)
```sql
SELECT PipelineDate FROM ConfigTable WHERE PipelineName = 'SalesPipeline'
````

ADF Activity:

```json
{
  "name": "LookupConfigDate",
  "type": "Lookup",
  "typeProperties": {
    "source": {
      "type": "SqlSource",
      "sqlReaderQuery": "SELECT TOP 1 PipelineDate FROM ConfigTable WHERE PipelineName = 'SalesPipeline'"
    },
    "dataset": {
      "referenceName": "AzureSql_ConfigDataset",
      "type": "DatasetReference"
    },
    "firstRowOnly": true
  }
}
```

➡️ Output:

```json
{
  "PipelineDate": "2025-09-12"
}
```

---

## 📊 Example 2: Lookup Multiple Rows (First Row Only = false)

```json
{
  "name": "LookupFileList",
  "type": "Lookup",
  "typeProperties": {
    "source": {
      "type": "BlobSource"
    },
    "dataset": {
      "referenceName": "Blob_FileListDataset",
      "type": "DatasetReference"
    },
    "firstRowOnly": false
  }
}
```

➡️ Output:

```json
[
  { "FileName": "sales_20250910.csv" },
  { "FileName": "sales_20250911.csv" },
  { "FileName": "sales_20250912.csv" }
]
```

---

## 📊 Example 3: Using Lookup Output in Another Activity

**Set Variable Activity** using Lookup output:

```json
{
  "name": "SetProcessDate",
  "type": "SetVariable",
  "typeProperties": {
    "variableName": "ProcessDate",
    "value": "@activity('LookupConfigDate').output.firstRow.PipelineDate"
  }
}
```

➡️ Assigns `ProcessDate` variable with the value retrieved from Lookup.

---

## 🚀 Workflow Example

**Scenario:** Retrieve file list and process each file.

1. **Lookup Activity** → Fetch file list from SQL table.
2. **ForEach Activity** → Loop through file list.
3. **Copy Activity** → Copy each file into staging.

Diagram:

```
Lookup (File List)
        ↓
     ForEach
        ↓
     Copy Data
```

---

## 🎯 Best Practices

* Use **FirstRowOnly = true** when fetching single config values.
* Use **FirstRowOnly = false** for lists (combine with ForEach).
* Keep queries efficient to avoid performance issues.
* Store **pipeline configs** in SQL tables and retrieve via Lookup.
* Always validate Lookup output before using it in downstream activities.

---

## 🏆 Key Takeaways

* **Lookup Activity** fetches configuration or data for pipelines.
* Supports both **single row** and **multi-row** outputs.
* Often used with **Set Variable, ForEach, If, or Stored Procedure activities**.
* Makes pipelines more **dynamic and parameter-driven**.

---
