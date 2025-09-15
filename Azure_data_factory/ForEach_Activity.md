# 🔁 ForEach Activity in Azure Data Factory (ADF)

---

## 📌 Introduction
The **ForEach Activity** in Azure Data Factory (ADF) is a **looping construct** that iterates over a **collection of items** and executes activities for each item.  
It is similar to a **for-each loop in programming** and is widely used for batch processing.

---

## ⚙️ Key Features
- Iterates through an **array or collection** (e.g., file names, child items, table list).  
- Executes **one or more activities** per iteration.  
- Supports **sequential** and **parallel execution**.  
- Useful for **dynamic pipelines** where the number of items may vary.  

---

## 🛠️ Properties

| Property              | Description |
|-----------------------|-------------|
| **Items**             | The array to iterate over (e.g., from pipeline parameter, variable, or Get Metadata output). |
| **Batch Count**       | Defines the maximum number of parallel executions (default = 20). |
| **IsSequential**      | If `true`, runs sequentially; if `false`, runs in parallel. |
| **Activities**        | List of activities to execute for each item. |

---

## 📊 Example 1: Loop Through a File List

### Input (Pipeline Parameter)
```json
"parameters": {
  "fileList": {
    "type": "Array",
    "defaultValue": ["sales.csv", "customer.csv", "product.csv"]
  }
}
````

### ForEach Configuration

* **Items:** `@pipeline().parameters.fileList`
* **Activity Inside Loop:** Copy Activity → Reads each file

### Output

* Iterates 3 times:

    * Loads `sales.csv`
    * Loads `customer.csv`
    * Loads `product.csv`

---

## 📊 Example 2: Loop Through Folder Contents

Use **Get Metadata Activity** to retrieve `childItems` from a folder, then loop with ForEach.

### Items

```json
"items": "@activity('GetMetadataFiles').output.childItems"
```

### Inside ForEach

* Copy Activity uses:

```json
"fileName": "@item().name"
```

---

## 📊 Example 3: Loop Through Table Names

Pipeline parameter provides list of tables:

```json
["Sales", "Customer", "Orders"]
```

ForEach executes Copy Activity for each table:

```json
"tableName": "@item()"
```

---

## 🚀 Workflow Example

**Scenario:** Load all files from a folder into Azure SQL Database.

1. **Get Metadata Activity** → Extract `childItems`.
2. **ForEach Activity** → Loop through files.
3. **Inside ForEach** → Copy Activity → Load each file into SQL.

Diagram:

```
Get Metadata (childItems)
        ↓
     ForEach
   ┌────────────┐
   │ Copy File1 │
   │ Copy File2 │
   │ Copy File3 │
   └────────────┘
```

---

## 🎯 Best Practices

* Use **parallelism** for faster performance (`IsSequential=false`, adjust `batchCount`).
* Use **sequential execution** when order matters (e.g., load dependencies).
* Avoid **large arrays** (e.g., thousands of items) as it can cause performance issues.
* Use **@item()** to access current iteration value.
* Combine with **Variables** or **Set Variable Activity** for dynamic file/table handling.

---

## 🏆 Key Takeaways

* **ForEach Activity** = Looping mechanism in ADF.
* Iterates over **arrays, child items, or pipeline parameters**.
* Supports **parallel & sequential** execution.
* Essential for scenarios like **multi-file ingestion, table migration, or schema iteration**.

---

