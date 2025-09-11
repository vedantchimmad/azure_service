# 🏗️ Pipeline Parameters in Azure Data Factory (ADF)

---

## 📌 Introduction
**Pipeline parameters** in Azure Data Factory (ADF) are **user-defined values** that are passed into a pipeline at **runtime**.  
They allow pipelines to be **dynamic, reusable, and configurable**, instead of hardcoding values like file names, table names, or folder paths.

Think of them as **inputs to your pipeline**, similar to function arguments in programming.

---

## ⚙️ Key Features
- Defined at the **pipeline level**.  
- Can be passed from **triggers, REST API calls, or manually** when running the pipeline.  
- Used inside **activities, datasets, and linked services**.  
- Support **string, int, bool, array, and object** types.  

---

## 🛠️ Defining Pipeline Parameters
Pipeline JSON Example:
```json
{
  "name": "SalesPipeline",
  "properties": {
    "parameters": {
      "fileName": { "type": "String" },
      "year": { "type": "Int" },
      "isTestRun": { "type": "Bool", "defaultValue": false }
    }
  }
}
````

---

## 🛠️ Using Pipeline Parameters

### 1️⃣ Inside Datasets

Pass pipeline parameter → dataset parameter:

```json
"parameters": {
  "fileName": { "type": "String" }
},
"typeProperties": {
  "fileName": "@pipeline().parameters.fileName"
}
```

---

### 2️⃣ Inside Activities

Used directly in expressions:

```json
"activities": [
  {
    "name": "CopyData",
    "type": "Copy",
    "inputs": [
      {
        "referenceName": "SalesDataset",
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

### 3️⃣ Inside Expressions

```text
@concat('sales_', pipeline().parameters.year, '.csv')
```

---

## 🔑 Example Scenarios

### 1️⃣ Dynamic File Ingestion

* **Pipeline Parameter:** `fileName = "sales_Jan.csv"`
* Pipeline runs and ingests only that file.

---

### 2️⃣ Environment Switching

* **Pipeline Parameter:** `env = "dev"`
* Switches connection strings dynamically:

    * If `env=dev` → Connect to Dev DB
    * If `env=prod` → Connect to Prod DB

---

### 3️⃣ Conditional Execution

```text
@pipeline().parameters.isTestRun
```

Used to control whether to execute certain activities (e.g., load to final table only in production).

---

## 📊 Example Workflow

**Pipeline Goal:** Load monthly sales data dynamically.

1. **Pipeline Parameter:** `monthName`.
2. **Dataset Parameter:** `fileName`.
3. Assign dynamically:
   `fileName = concat('sales_', pipeline().parameters.monthName, '.csv')`.

Diagram:

```
Pipeline Parameter (monthName = 'Jan')
        ↓
Dataset Parameter (fileName = 'sales_Jan.csv')
        ↓
Copy Activity (Loads File to SQL)
```

---

## 🚀 Example JSON Snippet

```json
{
  "name": "CopyPipeline",
  "properties": {
    "parameters": {
      "monthName": { "type": "String" }
    },
    "activities": [
      {
        "name": "CopySales",
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

* Always set **default values** for testing/debugging.
* Use pipeline parameters for **dynamic filenames, folders, and table names**.
* Combine with **dataset and linked service parameters** for full flexibility.
* Avoid passing sensitive info directly → use **Key Vault** for secrets.

---

## 🏆 Key Takeaways

* **Pipeline parameters** = inputs that make pipelines **dynamic**.
* Can be used in **datasets, activities, and linked services**.
* Support multiple data types (`string, int, bool, array, object`).
* Essential for **scalable, reusable, and environment-independent** pipelines.

---
