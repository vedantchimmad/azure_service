# 📂 Get Metadata Activity in Azure Data Factory (ADF)

---

## 📌 Introduction
The **Get Metadata Activity** in Azure Data Factory (ADF) is used to **retrieve metadata information** about files, folders, databases, or tables.  
It helps in **dynamic pipelines** where decisions depend on the **structure or properties of data sources**.

---

## ⚙️ Key Features
- Retrieves metadata about:
  - Files (size, name, last modified, etc.)
  - Folders (child items, existence, etc.)
  - Tables (columns, schema, structure)
- Supports **dynamic runtime decisions**.
- Can be combined with **If Condition, ForEach, Switch, and Until** activities.  

---

## 🛠️ Metadata Activity Properties

| Property         | Description |
|------------------|-------------|
| **Dataset**      | Dataset from which metadata is retrieved (e.g., Azure Blob, ADLS, SQL Table). |
| **Field List**   | List of metadata fields to extract (e.g., `size`, `lastModified`, `childItems`). |
| **Output**       | JSON object with metadata values (used by other activities). |

---

## 🛠️ Common Metadata Fields

### For **Files**
| Field            | Description |
|------------------|-------------|
| `size`           | File size in bytes. |
| `lastModified`   | Last modified timestamp. |
| `itemName`       | File name. |
| `exists`         | Returns `true` if file exists, else `false`. |

### For **Folders**
| Field            | Description |
|------------------|-------------|
| `childItems`     | List of files/folders inside. |
| `exists`         | Returns `true` if folder exists. |
| `lastModified`   | Last modified timestamp. |

### For **Tables**
| Field            | Description |
|------------------|-------------|
| `structure`      | Column names and data types. |
| `columnCount`    | Total number of columns. |
| `exists`         | Returns `true` if table exists. |

---

## 📊 Example: File Metadata

### Input
- Dataset: Azure Blob Storage (pointing to `/input/sales.csv`)
- Field List: `size`, `lastModified`, `itemName`

### Output
```json
{
  "size": 2048,
  "lastModified": "2025-09-11T08:23:00Z",
  "itemName": "sales.csv"
}
````

---

## 📊 Example: Folder Metadata

### Input

* Dataset: Azure Data Lake Storage (pointing to `/input/`)
* Field List: `childItems`

### Output

```json
{
  "childItems": [
    { "name": "sales.csv", "type": "File" },
    { "name": "customer.csv", "type": "File" },
    { "name": "archive", "type": "Folder" }
  ]
}
```

---

## 📊 Example: Table Metadata

### Input

* Dataset: Azure SQL Database (pointing to `SalesTable`)
* Field List: `structure`, `columnCount`

### Output

```json
{
  "structure": [
    { "name": "SaleID", "type": "int" },
    { "name": "Region", "type": "string" },
    { "name": "Amount", "type": "decimal" }
  ],
  "columnCount": 3
}
```

---

## 🛠️ Usage Scenarios

1. **Check if a file exists before processing**

    * Use `exists` property → proceed if `true`.
2. **Iterate over files in a folder**

    * Use `childItems` with **ForEach activity**.
3. **Dynamic schema detection**

    * Use `structure` for **schema drift** scenarios.
4. **Conditional execution**

    * Use `If Condition` activity with metadata output.
5. **File-based partitioning**

    * Extract file name or timestamp for dynamic output paths.

---

## 🚀 Example Workflow

**Scenario:** Load daily sales files only if they exist.

1. **Get Metadata Activity** (point to `/input/sales_20250912.csv`).
2. Retrieve `exists` property.
3. Use **If Condition Activity**:

    * If `exists = true` → Run Copy Activity.
    * Else → Skip or log message.

---

## 🎯 Best Practices

* Always check **exists** before processing to avoid pipeline failures.
* For large folders, avoid retrieving `childItems` unless necessary (can be slow).
* Use **Metadata Activity + ForEach** for batch ingestion scenarios.
* Store metadata output in **variables** for reuse across pipeline.

---

## 🏆 Key Takeaways

* **Get Metadata Activity** retrieves properties of files, folders, and tables.
* Common fields: `size`, `lastModified`, `exists`, `childItems`, `structure`.
* Essential for **dynamic, conditional, and schema-driven pipelines**.
* Best paired with **If Condition, Switch, and ForEach activities**.

---
