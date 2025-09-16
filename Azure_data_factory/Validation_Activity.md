# 📝 Validation Activity in Azure Data Factory (ADF)

---

## 📌 Introduction
The **Validation Activity** in ADF is used to **check the existence and readiness of data** before pipeline execution proceeds.  
It ensures that files, tables, or datasets are available and accessible before downstream processing begins.

---

## ⚙️ Key Features
- Verifies **data availability** before execution.  
- Supports **file existence checks** (Blob, ADLS, etc.) and **table readiness** (SQL, Synapse).  
- Allows configuration of **timeout** and **retry intervals**.  
- Prevents pipeline failure due to **missing or incomplete data**.  

---

## 🛠️ Properties

| Property              | Description |
|-----------------------|-------------|
| **Dataset**           | The dataset to validate (Blob, SQL, etc.). |
| **Child Items**       | Whether to validate child items (subfolders/files). |
| **Timeout**           | Maximum wait time before failing (in seconds). |
| **Sleep**             | Interval between retries (in seconds). |

---

## 📊 Example 1: Validate File Existence
```json
{
  "name": "ValidateSalesFile",
  "type": "Validation",
  "typeProperties": {
    "dataset": {
      "referenceName": "SalesBlobDataset",
      "type": "DatasetReference"
    },
    "childItems": false,
    "timeout": "00:05:00",
    "sleep": "00:00:30"
  }
}
````

➡️ Waits up to **5 minutes**, checking every **30 seconds** for the file to appear.

---

## 📊 Example 2: Validate Folder with Child Items

```json
{
  "name": "ValidateFolder",
  "type": "Validation",
  "typeProperties": {
    "dataset": {
      "referenceName": "InputFolderDataset",
      "type": "DatasetReference"
    },
    "childItems": true,
    "timeout": "00:10:00",
    "sleep": "00:01:00"
  }
}
```

➡️ Validates if the folder and its child files exist before proceeding.

---

## 🚀 Workflow Example

**Scenario:** Copy files only after they arrive in storage.

1. **Validation Activity** → Check if `sales_20250912.csv` exists.
2. **Copy Activity** → Move file into staging.
3. **Stored Procedure Activity** → Update table with new file data.

Diagram:

```
Validation → Copy Data → Stored Procedure
```

---

## 🎯 Best Practices

* Always configure **timeout** and **sleep interval** to avoid infinite waits.
* Use when **file arrival times vary** (batch pipelines).
* Combine with **Wait Activity** if additional delay is needed after validation.
* For real-time scenarios, consider **event-based triggers** instead of validation.

---

## 🏆 Key Takeaways

* **Validation Activity** ensures datasets/files are ready before processing.
* Helps avoid pipeline failures due to missing data.
* Supports **file/folder existence, table readiness, and child item checks**.
* Makes pipelines **more reliable and resilient** in data-dependent workflows.

---
