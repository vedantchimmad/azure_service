# ⚙️ Parameterization in Azure Data Factory (ADF)

---

## 📌 Introduction
**Parameterization in ADF** allows you to build **dynamic, reusable, and flexible pipelines** by passing values at runtime.  
Instead of hardcoding values (like file names, folder paths, connection strings, or table names), you use **parameters** that can be set:  
- At **pipeline level**  
- At **activity level**  
- At **dataset level**  
- At **linked service level**  

---

## 🎯 Benefits of Parameterization
- Avoids hardcoding → improves **reusability**.  
- Enables **dynamic pipelines** (e.g., load multiple files/tables).  
- Simplifies management across environments (**Dev, Test, Prod**).  
- Makes ADF pipelines **scalable** and easier to maintain.  

---

## 🛠️ Types of Parameterization in ADF

### 1️⃣ **Pipeline Parameters**
- Defined at pipeline level.  
- Passed when triggering pipeline.  
- Accessible inside activities, datasets, and linked services.  

```json
"parameters": {
  "fileName": { "type": "String" },
  "year": { "type": "Int" }
}
````

Usage inside activity:

```json
"fileName": "@pipeline().parameters.fileName"
```

---

### 2️⃣ **Activity Parameters**

* Specific to an **activity (e.g., Copy, Lookup, ForEach)**.
* Control behavior of an activity dynamically.

Example:

```json
"activities": [
  {
    "name": "CopyData",
    "type": "Copy",
    "inputs": [
      {
        "referenceName": "BlobDataset",
        "type": "DatasetReference",
        "parameters": {
          "fileName": "@pipeline().parameters.fileName"
        }
      }
    ]
  }
]
```

---

### 3️⃣ **Dataset Parameters**

* Used to make datasets dynamic (e.g., file name, folder path, table name).
* Values assigned from pipeline or activity.

Example:

```json
"parameters": {
  "folderPath": { "type": "String" },
  "fileName": { "type": "String" }
}
```

Usage inside dataset:

```json
"folderPath": "@dataset().folderPath",
"fileName": "@dataset().fileName"
```

---

### 4️⃣ **Linked Service Parameters**

* Used for **connection details** (server name, database name, schema).
* Useful for deploying pipelines across multiple environments.

Example:

```json
"parameters": {
  "DBName": { "type": "String" }
}
```

Usage:

```json
"database": "@linkedService().DBName"
```

---

## 🔑 Example Scenario

### Goal: Load multiple sales files dynamically

1. **Pipeline Parameter:** `monthName`.
2. **Dataset Parameter:** `fileName`.
3. **Copy Activity:** Pass `fileName = concat('sales_', pipeline().parameters.monthName, '.csv')`.
4. Output goes to SQL table with parameterized table name.

Diagram:

```
📂 Blob Storage (sales_Jan.csv, sales_Feb.csv...)
      ↓
🛠️ Dataset (Parameterized File Name)
      ↓
📊 Copy Activity (Pipeline Param → Dataset Param)
      ↓
SQL Database (Dynamic Table)
```

---

## 🚀 Example JSON Snippet

```json
{
  "name": "SalesPipeline",
  "properties": {
    "parameters": {
      "monthName": { "type": "String" }
    },
    "activities": [
      {
        "name": "CopySalesData",
        "type": "Copy",
        "inputs": [
          {
            "referenceName": "SalesDataset",
            "type": "DatasetReference",
            "parameters": {
              "fileName": "@concat('sales_', pipeline().parameters.monthName, '.csv')"
            }
          }
        ],
        "outputs": [
          {
            "referenceName": "SQLDataset",
            "type": "DatasetReference",
            "parameters": {
              "tableName": "@concat('Sales_', pipeline().parameters.monthName)"
            }
          }
        ]
      }
    ]
  }
}
```

---

## 🎯 Best Practices

* Always provide **default values** for testing.
* Use **linked service parameters** for **environment migration** (Dev → Test → Prod).
* Combine **pipeline + dataset parameters** for flexible file/table selection.
* Use `@concat()`, `@pipeline().parameters`, `@dataset().paramName` expressions for dynamic values.

---

## 🏆 Key Takeaways

* **Parameterization** makes ADF pipelines **dynamic and reusable**.
* Can be applied at **Pipeline, Activity, Dataset, and Linked Service levels**.
* Essential for **handling dynamic files, tables, and environments**.
* Reduces duplication and **improves maintainability**.

---
