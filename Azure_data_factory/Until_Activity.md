# 📝 Until Activity in Azure Data Factory (ADF)

---

## 📌 Introduction
The **Until Activity** in Azure Data Factory (ADF) is a **looping construct** that executes one or more activities **repeatedly until a specified condition evaluates to true**.  
It is similar to a **while loop in programming** and is useful for **polling, retries, or waiting for external conditions**.

---

## ⚙️ Key Features
- Loops until a **boolean expression** evaluates to `true`.  
- Supports **timeout** and **delay** between iterations.  
- Can contain multiple activities inside the loop.  
- Useful for **waiting on file availability, monitoring job completion, or retrying failed tasks**.  

---

## 🛠️ Properties

| Property       | Description |
|----------------|-------------|
| **Expression** | Boolean expression to check loop exit condition. |
| **Timeout**    | Maximum run duration before the loop is forced to stop. |
| **Delay**      | Pause duration between iterations (in seconds). |
| **Activities** | The activities to execute inside the loop. |

---

## 📊 Example 1: Simple Until Loop
```json
{
  "name": "UntilExample",
  "type": "Until",
  "typeProperties": {
    "expression": "@equals(pipeline().variables.IsFileReady, true)",
    "timeout": "00:10:00",
    "delay": "00:01:00"
  },
  "activities": [
    {
      "name": "CheckFileStatus",
      "type": "Lookup",
      "typeProperties": {
        "dataset": {
          "referenceName": "FileStatusDataset",
          "type": "DatasetReference"
        }
      }
    }
  ]
}
````

➡️ Repeats **CheckFileStatus** every **1 minute** until `IsFileReady = true` or **10 minutes timeout**.

---

## 📊 Example 2: Polling for File Arrival

```json
{
  "name": "UntilFileArrives",
  "type": "Until",
  "typeProperties": {
    "expression": "@greater(length(activity('GetMetadataFile').output.childItems), 0)",
    "timeout": "00:30:00",
    "delay": "00:05:00"
  },
  "activities": [
    {
      "name": "GetMetadataFile",
      "type": "GetMetadata",
      "typeProperties": {
        "dataset": {
          "referenceName": "InputFolderDataset",
          "type": "DatasetReference"
        }
      }
    }
  ]
}
```

➡️ Checks every **5 minutes** for file arrival in the folder, stops after **30 minutes** if not found.

---

## 📊 Example 3: Retrying Copy Until Success

```json
{
  "name": "RetryCopyUntilSuccess",
  "type": "Until",
  "typeProperties": {
    "expression": "@equals(activity('CopyActivity').status, 'Succeeded')",
    "timeout": "00:20:00",
    "delay": "00:02:00"
  },
  "activities": [
    {
      "name": "CopyActivity",
      "type": "Copy",
      "typeProperties": {
        "source": { "type": "BlobSource" },
        "sink": { "type": "SqlSink" }
      }
    }
  ]
}
```

➡️ Retries copy operation every **2 minutes** until it succeeds or **20-minute timeout** is reached.

---

## 🚀 Workflow Example

**Scenario:** Wait for a dependent job to finish before loading data.

1. **Until Activity** → Polls job status every 2 minutes.
2. **If Condition** → If job complete, proceed to Copy Data.
3. **Copy Activity** → Load processed data.

Diagram:

```
Until (Check Job Status)
       ↓
   If Job Done?
       ↓
    Copy Data
```

---

## 🎯 Best Practices

* Always configure a **timeout** to avoid infinite loops.
* Use **delay** wisely to avoid excessive resource usage.
* Keep loop activities **lightweight** (Lookup, Metadata, Validation).
* Use for **polling scenarios**, but prefer **event triggers** if available.

---

## 🏆 Key Takeaways

* **Until Activity** loops until a condition is true.
* Useful for **polling, retries, waiting on files, or external jobs**.
* Supports **timeout** and **delay** to control loop behavior.
* Helps make pipelines **robust and fault-tolerant**.

---
