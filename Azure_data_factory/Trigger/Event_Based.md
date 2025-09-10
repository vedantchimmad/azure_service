# 📡 Event-based Trigger in Azure Data Factory (ADF)

---

## 📌 Introduction
An **Event-based Trigger** in Azure Data Factory (ADF) allows pipelines to run **in real time** when a **data event occurs**.  
It is commonly used for **event-driven ingestion** where pipelines start as soon as new data lands in storage.

---

## ⚙️ Key Features
- Executes pipelines **immediately when an event occurs**.  
- Supports **Azure Blob Storage** and **ADLS Gen2** events.  
- Monitors file operations such as:
  - **BlobCreated** → Trigger when a new file is uploaded.  
  - **BlobDeleted** → Trigger when a file is removed.  
- Can filter events based on:
  - File **path pattern** (`input/*.csv`).  
  - **File type** or folder location.  
- **No polling needed** → Uses **Azure Event Grid** for efficiency.  

---

## 🛠️ Properties
| Property            | Description |
|---------------------|-------------|
| **scope**           | Storage account or container to monitor. |
| **events**          | Events to capture (`Microsoft.Storage.BlobCreated`, `Microsoft.Storage.BlobDeleted`). |
| **subjectBeginsWith** | Filters events by file path prefix (e.g., `/container/input/`). |
| **subjectEndsWith**   | Filters events by file name suffix (e.g., `.csv`). |
| **pipelines**       | Pipelines linked to the trigger. |

---

## 🔑 JSON Example (Blob Created Event)
```json
{
  "name": "BlobEventTrigger",
  "properties": {
    "type": "BlobEventsTrigger",
    "typeProperties": {
      "scope": "/subscriptions/{subId}/resourceGroups/{rg}/providers/Microsoft.Storage/storageAccounts/{storageName}",
      "events": [ "Microsoft.Storage.BlobCreated" ],
      "subjectBeginsWith": "/mycontainer/input/",
      "subjectEndsWith": ".csv"
    },
    "pipelines": [
      {
        "pipelineReference": {
          "referenceName": "Pipeline_ProcessUploadedFile",
          "type": "PipelineReference"
        }
      }
    ]
  }
}
````

---

## 🚀 Example Scenarios

### 1️⃣ Process Files When Uploaded

* Monitor `raw/input/` folder.
* Trigger when `.csv` file is uploaded.
* Pipeline processes the file → Loads into Data Lake or SQL.

---

### 2️⃣ Clean Up When File Deleted

* Monitor container for **BlobDeleted** event.
* Trigger pipeline to **update metadata** or remove dependent records.

---

### 3️⃣ Multiple File Types

* Trigger for both `.csv` and `.json` files.
* Use `subjectEndsWith` to differentiate processing pipelines.

---

## 📊 When to Use

* **Real-time ingestion** (IoT, streaming logs, transaction files).
* **Data Lake pipelines** → Start as soon as a new file arrives.
* **Change Data Capture (CDC)** → Detect file-level changes.
* **Automated workflows** → e.g., start ML model scoring once new training data is uploaded.

---

## 🎯 Key Takeaways

* **Event-based Trigger** = **real-time, event-driven execution**.
* Eliminates **latency of scheduled triggers**.
* Filters by **prefix/suffix** to run only on relevant files.
* Best for **real-time pipelines** that depend on **new or deleted files**.

---
