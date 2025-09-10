# ⏱️ Types of Triggers in Azure Data Factory (ADF)

---

## 📌 Introduction
In **Azure Data Factory (ADF)**, a **trigger** is a mechanism that **automatically executes pipelines** based on conditions.  
Triggers define **when and how a pipeline runs**.  

There are **three main types of triggers** in ADF.

---

## 🔑 Types of Triggers

### 1️⃣ **Schedule Trigger**
- Runs pipelines on a **predefined schedule**.  
- Supports:
  - Specific **start and end times**.  
  - **Recurrence** (minutes, hours, days, weeks, months).  
  - Time zone selection.  

✅ Example:  
- Run a pipeline **every day at 6 AM IST**.  

```json
{
  "name": "DailyTrigger",
  "properties": {
    "type": "ScheduleTrigger",
    "typeProperties": {
      "recurrence": {
        "frequency": "Day",
        "interval": 1,
        "startTime": "2025-09-08T06:00:00Z",
        "timeZone": "India Standard Time"
      }
    }
  }
}
````

---

### 2️⃣ **Tumbling Window Trigger**

* Runs pipelines at **fixed, contiguous, and non-overlapping time intervals**.
* Ensures **exactly-once execution** within each window.
* Useful for **time-sliced data processing** (hourly/daily ingestion).
* Supports **dependency chaining** (trigger one window after another completes).

✅ Example:

* Process hourly sales data → Each trigger handles **one hour window**.

```json
{
  "name": "HourlyTumblingTrigger",
  "properties": {
    "type": "TumblingWindowTrigger",
    "typeProperties": {
      "frequency": "Hour",
      "interval": 1,
      "startTime": "2025-09-08T00:00:00Z",
      "maxConcurrency": 1
    }
  }
}
```

---

### 3️⃣ **Event-based Trigger**

* Executes pipelines when **an event occurs** in storage.
* Supports:

    * **Blob Storage** events (file added/modified/deleted).
    * **ADLS Gen2** events.
* Useful for **real-time ingestion** (e.g., process file immediately after upload).

✅ Example:

* Trigger pipeline when a **CSV file is uploaded** into a Blob container.

```json
{
  "name": "BlobEventTrigger",
  "properties": {
    "type": "BlobEventsTrigger",
    "typeProperties": {
      "scope": "/subscriptions/{subId}/resourceGroups/{rg}/providers/Microsoft.Storage/storageAccounts/{storageName}",
      "events": [ "Microsoft.Storage.BlobCreated" ]
    }
  }
}
```

---

## 📊 Trigger Comparison

| Trigger Type         | Use Case                                | Example             |
| -------------------- | --------------------------------------- | ------------------- |
| **Schedule Trigger** | Run pipelines on fixed schedule         | Daily load at 6 AM  |
| **Tumbling Window**  | Time-based data slicing with dependency | Hourly sales data   |
| **Event-based**      | Real-time processing on event arrival   | File upload to Blob |

---

## 🎯 Key Takeaways

* **Schedule Trigger** → Best for fixed, periodic jobs.
* **Tumbling Window Trigger** → Best for time-partitioned datasets (batch processing).
* **Event-based Trigger** → Best for real-time, event-driven pipelines.
* You can **combine multiple triggers** on the same pipeline.

---
