# 🗑️ Delete Activity in Azure Data Factory (ADF)

---
## 📌 Introduction
The **Delete Activity** in Azure Data Factory (ADF) is used to **delete files or folders from data stores**.  
It is typically used for:
- Cleaning up temporary or staging data.  
- Managing data retention policies.  
- Removing files after processing.  

---

## ⚙️ How It Works
1. Connects to a **data source** (e.g., Blob, ADLS, File Share, SFTP).  
2. Deletes files or folders based on **wildcards, partition paths, or metadata conditions**.  
3. Can be combined with **Copy/Move Activities** for end-to-end workflows.  

---

## 🛠️ Syntax (Pipeline JSON Example)
```json
{
  "name": "DeleteOldFiles",
  "properties": {
    "activities": [
      {
        "name": "DeleteFilesActivity",
        "type": "Delete",
        "typeProperties": {
          "dataset": {
            "referenceName": "BlobDataset",
            "type": "DatasetReference"
          },
          "recursive": true
        }
      }
    ]
  }
}
````

---

## 🔑 Key Properties

| Property                     | Description                                                         |
| ---------------------------- | ------------------------------------------------------------------- |
| **dataset**                  | Dataset reference pointing to storage.                              |
| **recursive**                | Boolean – whether to delete files recursively inside folders.       |
| **enableLogging**            | Boolean – enables deletion log.                                     |
| **maxConcurrentConnections** | Controls parallel deletion.                                         |
| **storeSettings**            | Allows settings like `wildcardFileName` or `modifiedDateStart/End`. |

---

## ⚡ Supported Data Stores

* **Azure Blob Storage**
* **Azure Data Lake Storage (ADLS Gen1/Gen2)**
* **Azure File Storage**
* **Amazon S3**
* **SFTP / FTP / File Systems**

---

## 🚀 Example Scenarios

### 1️⃣ Delete Files Older Than 7 Days

Use **Delete Activity + Get Metadata**:

* `Get Metadata Activity` → Retrieve last modified date.
* `If Condition` → If older than 7 days, run **Delete Activity**.

---

### 2️⃣ Delete All Processed Files

* After a **Copy Activity**, run **Delete Activity** to remove source files.

```json
{
  "name": "DeleteProcessedFiles",
  "type": "Delete",
  "typeProperties": {
    "dataset": {
      "referenceName": "ProcessedBlobDataset",
      "type": "DatasetReference"
    },
    "recursive": false
  }
}
```

---

### 3️⃣ Delete Folder Recursively

```json
{
  "name": "DeleteFolder",
  "type": "Delete",
  "typeProperties": {
    "dataset": {
      "referenceName": "FolderDataset",
      "type": "DatasetReference"
    },
    "recursive": true
  }
}
```

---

## 📊 Best Practices

* Use **wildcards** (`*.csv`, `2024/*`) for pattern-based deletes.
* Always test deletes in a **non-production environment**.
* Enable **logging** for audit and tracking.
* Combine with **Validation Activity** to ensure file exists before deletion.

---

## 🎯 Key Takeaways

* **Delete Activity** helps maintain storage hygiene by removing unused/old data.
* Supports **conditional deletes, recursive folder cleanup, and wildcards**.
* Often paired with **Copy, Move, or Metadata activities** in pipelines.

---
