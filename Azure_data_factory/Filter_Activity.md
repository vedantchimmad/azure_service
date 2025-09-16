# 📝 Filter Activity in Azure Data Factory (ADF)

---

## 📌 Introduction
The **Filter Activity** in ADF is used to **filter items from an array** based on a **boolean condition (expression)**.  
It allows you to select only the elements that meet specific criteria, similar to the **WHERE clause in SQL** or the **filter() function in programming**.

---

## ⚙️ Key Features
- Works only on **array variables or array outputs** (e.g., Lookup, Get Metadata).  
- Applies a **predicate expression** to filter items.  
- Returns a new **array with matching elements**.  
- Commonly used with **ForEach Activity** to loop only through filtered items.  

---

## 🛠️ Properties

| Property   | Description |
|------------|-------------|
| **Items**  | The input array (variable or activity output). |
| **Condition** | The expression to evaluate (must return true/false). |

---

## 📊 Example 1: Filter Files by Extension
Input Array (from Lookup or Metadata):
```json
[
  { "name": "sales_20250910.csv" },
  { "name": "sales_20250911.json" },
  { "name": "sales_20250912.csv" }
]
````

Filter Activity:

```json
{
  "name": "FilterCSVFiles",
  "type": "Filter",
  "typeProperties": {
    "items": "@activity('GetFileList').output.value",
    "condition": "@endswith(item().name, '.csv')"
  }
}
```

➡️ Output:

```json
[
  { "name": "sales_20250910.csv" },
  { "name": "sales_20250912.csv" }
]
```

---

## 📊 Example 2: Filter Files by Size

```json
{
  "name": "FilterLargeFiles",
  "type": "Filter",
  "typeProperties": {
    "items": "@activity('GetMetadataFiles').output.childItems",
    "condition": "@greater(item().size, 1000000)"
  }
}
```

➡️ Keeps only files **larger than 1 MB**.

---

## 📊 Example 3: Filter Active Records

```json
{
  "name": "FilterActiveUsers",
  "type": "Filter",
  "typeProperties": {
    "items": "@activity('LookupUsers').output.value",
    "condition": "@equals(item().status, 'Active')"
  }
}
```

➡️ Keeps only users with `status = Active`.

---

## 🚀 Workflow Example

**Scenario:** Process only `.csv` files from a folder.

1. **Get Metadata Activity** → Retrieve file list.
2. **Filter Activity** → Select `.csv` files only.
3. **ForEach Activity** → Process filtered files.

Diagram:

```
Get Metadata → Filter (CSV files) → ForEach → Copy Data
```

---

## 🎯 Best Practices

* Always ensure input to Filter Activity is an **array**.
* Use **string functions** (`startswith`, `endswith`, `contains`) for filtering file names.
* Use **logical operators** (`and`, `or`, `not`) for complex conditions.
* Combine with **ForEach** for iterating over filtered results.

---

## 🏆 Key Takeaways

* **Filter Activity** extracts a subset of array items based on conditions.
* Works well with **Lookup** and **Get Metadata** outputs.
* Enables **dynamic, rule-based selection** of items in pipelines.
* Improves efficiency by processing only **relevant data**.

---
