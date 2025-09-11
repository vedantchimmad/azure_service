# 🛠️ Dataset Parameterization in Azure Data Factory (ADF)

---

## 📌 Introduction
**Dataset parameterization** in Azure Data Factory (ADF) allows you to create **dynamic datasets** by passing values (parameters) at runtime.  
Instead of hardcoding file names, paths, or table names, you define **parameters** inside a dataset and assign them values when the pipeline runs.  

This makes pipelines **flexible, reusable, and scalable**.  

---

## ⚙️ Why Use Dataset Parameters?
- Avoid hardcoding values like file names, table names, or paths.  
- Reuse the same dataset for **multiple sources/sinks**.  
- Enable **dynamic pipelines** for different environments (dev, test, prod).  
- Improve maintainability and reduce duplication.  

---

## 🛠️ Steps to Parameterize a Dataset

### 1️⃣ Create a Dataset
- In ADF studio → Go to **Manage → Datasets**.  
- Choose dataset type (e.g., Blob Storage, SQL DB).  

---

### 2️⃣ Add Parameters
- Open dataset → **Parameters tab** → Add parameters like:  
  - `folderPath`  
  - `fileName`  
  - `tableName`  

---

### 3️⃣ Use Parameters in Dataset Properties
Example for **Azure Blob Storage dataset**:  
```json
{
  "name": "BlobDataset",
  "properties": {
    "linkedServiceName": { "referenceName": "AzureBlobLS", "type": "LinkedServiceReference" },
    "parameters": {
      "folderPath": { "type": "String" },
      "fileName": { "type": "String" }
    },
    "type": "Binary",
    "typeProperties": {
      "location": {
        "type": "AzureBlobStorageLocation",
        "folderPath": "@dataset().folderPath",
        "fileName": "@dataset().fileName"
      }
    }
  }
}
````

---

### 4️⃣ Pass Parameters from Pipeline

* In the **pipeline activity**, assign values to dataset parameters.

Example:

```json
{
  "name": "CopyData",
  "type": "Copy",
  "typeProperties": {
    "source": { "type": "DelimitedTextSource" },
    "sink": { "type": "SqlSink" }
  },
  "inputs": [
    {
      "referenceName": "BlobDataset",
      "type": "DatasetReference",
      "parameters": {
        "folderPath": "input/2025/",
        "fileName": "sales.csv"
      }
    }
  ]
}
```

---

## 🔑 Example Use Cases

### 1️⃣ Dynamic File Names

* Dataset parameter: `fileName`.
* Pipeline assigns `"sales_@pipeline().parameters.runDate.csv"`.

---

### 2️⃣ Dynamic Folder Paths

* Dataset parameter: `folderPath`.
* Use `concat('input/', pipeline().parameters.year, '/', pipeline().parameters.month)`

---

### 3️⃣ Dynamic Tables

* Dataset parameter: `tableName`.
* Used in SQL dataset to copy data into different tables dynamically.

---

## 📊 Example Workflow

**Pipeline Goal:** Load multiple monthly files dynamically.

1. **Pipeline parameter:** `monthName`.
2. **Dataset parameter:** `fileName`.
3. Assign value → `fileName = concat('sales_', pipeline().parameters.monthName, '.csv')`.
4. Copy activity runs dynamically for each month’s file.

Diagram:

```
📂 Blob Storage (sales_Jan.csv, sales_Feb.csv...)
      ↓
🛠️ Dataset with Parameterized File Name
      ↓
📊 Copy Activity
      ↓
SQL Database (SalesData)
```

---

## 🎯 Best Practices

* Use **dataset parameters** instead of duplicating multiple datasets.
* Combine with **pipeline parameters** for **end-to-end dynamic pipelines**.
* Always provide **default values** for testing.
* Use `concat()` and `@pipeline().parameters` expressions for flexible file/table naming.

---

## 🏆 Key Takeaways

* **Dataset parameterization** = Reusable datasets with dynamic values.
* Helps in handling **dynamic paths, files, and tables**.
* Reduces **hardcoding and duplication**.
* Essential for **scalable and flexible ADF pipelines**.

---
