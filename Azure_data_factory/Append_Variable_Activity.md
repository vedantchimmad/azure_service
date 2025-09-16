# 📝 Append Variable Activity in Azure Data Factory (ADF)

---

## 📌 Introduction
The **Append Variable Activity** in ADF is used to **add a new value to the end of an array variable**.  
It is commonly used for **collecting lists of items** (e.g., file names, IDs, or row counts) during pipeline execution.

---

## ⚙️ Key Features
- Works **only with array variables**.  
- Appends (adds) a value without overwriting existing items.  
- Values can be **static** or **dynamic expressions**.  
- Useful for **iteration scenarios** with `ForEach`.  

---

## 🛠️ Properties

| Property   | Description |
|------------|-------------|
| **Name**   | The name of the array variable. |
| **Value**  | The value to append (can be a string, int, object, or expression). |

---

## 🛠️ Defining Array Variables
Before using Append Variable, define an **array variable** in the pipeline:

```json
"variables": {
  "FileList": { "type": "Array", "defaultValue": [] },
  "FailedFiles": { "type": "Array", "defaultValue": [] }
}
````

---

## 📊 Example 1: Append Static Value

```json
{
  "name": "AppendFile",
  "type": "AppendVariable",
  "typeProperties": {
    "variableName": "FileList",
    "value": "sales_20250912.csv"
  }
}
```

➡️ If `FileList = []`, after execution → `["sales_20250912.csv"]`.

---

## 📊 Example 2: Append Dynamic Value

```json
{
  "name": "AppendDynamicFile",
  "type": "AppendVariable",
  "typeProperties": {
    "variableName": "FileList",
    "value": "@concat('sales_', formatDateTime(utcnow(),'yyyyMMdd'), '.csv')"
  }
}
```

➡️ Appends today’s file name: `["sales_20250912.csv"]`.

---

## 📊 Example 3: Append from Activity Output

```json
{
  "name": "AppendRowCount",
  "type": "AppendVariable",
  "typeProperties": {
    "variableName": "FailedFiles",
    "value": "@activity('GetMetadataActivity').output.itemName"
  }
}
```

➡️ Appends file name retrieved by **Get Metadata Activity**.

---

## 🚀 Workflow Example

**Scenario:** Collect all processed file names.

1. Use **Get Metadata Activity** to get file list.
2. Use **ForEach Activity** to loop through each file.
3. Inside ForEach → **Append Variable Activity** → add file name to `FileList`.
4. At end of pipeline, `FileList` contains all processed files.

Diagram:

```
Get Metadata (list of files)
            ↓
        ForEach File
            ↓
   Append Variable → FileList
```

---

## 🎯 Best Practices

* Initialize array variables with `[]` to avoid errors.
* Use Append Variable inside **ForEach** to build collections.
* For large datasets, avoid storing excessive values in variables (consider storage account or SQL instead).
* Keep variable names meaningful (`ProcessedFiles`, `FailedFiles`, `SuccessIds`).

---

## 🏆 Key Takeaways

* **Append Variable Activity** adds values to an array variable.
* Works with **static values, dynamic expressions, or activity outputs**.
* Best suited for **building lists in iterations**.
* Complements **Set Variable Activity**, which assigns or overwrites values.

---

