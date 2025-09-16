# 📝 Set Variable Activity in Azure Data Factory (ADF)

---

## 📌 Introduction
The **Set Variable Activity** in Azure Data Factory (ADF) is used to **assign or update the value of a variable** during pipeline execution.  
It works like variable assignment in programming and is essential for **dynamic pipelines**.

---

## ⚙️ Key Features
- Assigns a **static value** or a **dynamic expression**.  
- Works with pipeline-defined variables (`String`, `Bool`, `Array`, `Object`).  
- Updates variable values at runtime.  
- Often used with **If, ForEach, Switch, and Until** activities.  

---

## 🛠️ Properties

| Property   | Description |
|------------|-------------|
| **Name**   | The name of the variable (must already be defined in pipeline). |
| **Value**  | The value to assign (can be a constant or expression). |

---

## 🛠️ Defining Variables
Before using Set Variable, define variables in the pipeline:

```json
"variables": {
  "FileName": { "type": "String" },
  "RowCount": { "type": "Int", "defaultValue": 0 },
  "IsProcessed": { "type": "Bool", "defaultValue": false },
  "FileList": { "type": "Array", "defaultValue": [] }
}
````

---

## 📊 Example 1: Assign File Name

```json
{
  "name": "SetFileName",
  "type": "SetVariable",
  "typeProperties": {
    "variableName": "FileName",
    "value": "sales_20250912.csv"
  }
}
```

➡️ Variable `FileName = sales_20250912.csv`

---

## 📊 Example 2: Assign Dynamic Value

```json
{
  "name": "SetDynamicFileName",
  "type": "SetVariable",
  "typeProperties": {
    "variableName": "FileName",
    "value": "@concat('sales_', formatDateTime(utcnow(),'yyyyMMdd'), '.csv')"
  }
}
```

➡️ Variable `FileName = sales_20250912.csv`

---

## 📊 Example 3: Assign From Metadata Output

```json
{
  "name": "SetRowCount",
  "type": "SetVariable",
  "typeProperties": {
    "variableName": "RowCount",
    "value": "@activity('GetMetadataActivity').output.size"
  }
}
```

➡️ Assigns file size from **Get Metadata Activity** output.

---

## 📊 Example 4: Update Boolean Variable

```json
{
  "name": "SetProcessFlag",
  "type": "SetVariable",
  "typeProperties": {
    "variableName": "IsProcessed",
    "value": "true"
  }
}
```

➡️ Variable `IsProcessed = true`.

---

## 🚀 Workflow Example

**Scenario:** Process a file only if it exists.

1. **Get Metadata Activity** → Check file existence.
2. **If Condition Activity**:

   * True → Set Variable `IsProcessed = true`.
   * False → Set Variable `IsProcessed = false`.

Diagram:

```
Get Metadata
      ↓
 If Condition (exists?)
 ┌───────────────┐
 │ True → SetVar │ (IsProcessed=true)
 │ False → SetVar│ (IsProcessed=false)
 └───────────────┘
```

---

## 🎯 Best Practices

* Always **define variables at pipeline level** before using them.
* Use **expressions** to assign dynamic values.
* For arrays, use **Append Variable Activity** (not Set Variable).
* Use **variables for state management** (flags, counters, file names).
* Keep variable names meaningful (`RowCount`, `IsValidFile`, `ProcessDate`).

---

## 🏆 Key Takeaways

* **Set Variable Activity** assigns or updates pipeline variables.
* Works with **String, Int, Bool, Object** types.
* Supports **static values, dynamic expressions, and activity outputs**.
* Ideal for **state tracking, file naming, and conditional logic**.

---
