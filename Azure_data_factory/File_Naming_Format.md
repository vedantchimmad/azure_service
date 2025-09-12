# 🗂️ File Naming in Azure Data Factory (ADF)

---

## 📌 Introduction
In Azure Data Factory (ADF), **file naming conventions** play a critical role in managing data pipelines.  
Using **dynamic file names** ensures that pipelines can handle **different datasets, partitions, and timestamps** automatically without manual intervention.

---

## ⚙️ Why File Naming is Important?
- Helps organize data (partitioned by **date, region, or type**).  
- Prevents overwriting of existing files.  
- Allows **incremental data loads**.  
- Makes **monitoring and troubleshooting** easier.  

---

## 🛠️ File Naming Options in ADF

### 1️⃣ Static File Naming
Hardcoded file name in the dataset or activity.  
```json
"fileName": "SalesReport.csv"
````

✔️ Simple but **not reusable** for dynamic scenarios.

---

### 2️⃣ Dynamic File Naming with Parameters

Use **dataset parameters** and pass values from pipeline.

```json
"fileName": "@dataset().fileName"
```

Pipeline → Dataset → File name parameterized.

---

### 3️⃣ File Naming with Pipeline Parameters

```json
"fileName": "@pipeline().parameters.inputFile"
```

When executing pipeline, provide:

* `inputFile = Sales_2025_01.csv`

---

### 4️⃣ Dynamic File Naming with System Variables

Use **system variables** to include runtime details.

```json
"fileName": "@concat('Sales_', pipeline().RunId, '.csv')"
```

| System Variable            | Description                     | Example                         |
| -------------------------- | ------------------------------- | ------------------------------- |
| `@pipeline().RunId`        | Unique ID for each pipeline run | `Sales_7f9c.csv`                |
| `@utcnow()`                | Current UTC date/time           | `Sales_2025-09-12T14-30-00.csv` |
| `@pipeline().parameters`   | Custom pipeline parameters      | `Sales_Jan.csv`                 |
| `@trigger().scheduledTime` | Trigger execution time          | `Sales_2025-09-12.csv`          |

---

### 5️⃣ File Naming with Expressions

Use ADF expressions to format names dynamically.

#### Example: Add Date Stamp

```json
"fileName": "@concat('Sales_', formatDateTime(utcnow(), 'yyyyMMdd'), '.csv')"
```

➡️ Output: `Sales_20250912.csv`

#### Example: Include Partition Info

```json
"fileName": "@concat('Sales_', pipeline().parameters.Region, '_', pipeline().parameters.Month, '.csv')"
```

➡️ Output: `Sales_East_Jan.csv`

---

## 📊 Example Use Case

### Scenario: Daily Sales Data Load

1. **Pipeline Parameter:** `Region`.
2. **Dynamic File Naming:**

```json
"fileName": "@concat('Sales_', pipeline().parameters.Region, '_', formatDateTime(utcnow(), 'yyyyMMdd'), '.csv')"
```

3. **Output File Example:**

    * `Sales_East_20250912.csv`
    * `Sales_West_20250912.csv`

---

## 🎯 Best Practices

* Always use **dynamic naming** for incremental data loads.
* Include **timestamps or partitions** in names to avoid overwrites.
* Follow a **consistent convention**:

  ```
  <Entity>_<Region>_<Date>.csv
  Customer_North_20250912.csv
  ```
* Use **system variables** for automation.
* Store **parameters at pipeline level** for better flexibility.

---

## 🏆 Key Takeaways

* File naming in ADF can be **static or dynamic**.
* Use **pipeline parameters + system variables + expressions** for automation.
* Dynamic naming prevents overwrites and helps organize data.
* Always adopt **clear and consistent naming conventions**.

---

