# 📅 Schedule Trigger in Azure Data Factory (ADF)

---

## 📌 Introduction
A **Schedule Trigger** in Azure Data Factory (ADF) allows you to **run pipelines on a recurring schedule**.  
It is best suited for **time-based batch processing** jobs (e.g., daily, weekly, or monthly runs).  

---

## ⚙️ Key Features
- Supports **start and end times**.  
- Can specify **recurrence intervals** (minutes, hours, days, weeks, months).  
- Uses **time zones** for scheduling accuracy.  
- Can run **multiple pipelines** with a single trigger.  

---

## 🛠️ Properties
| Property        | Description |
|-----------------|-------------|
| **recurrence**  | Defines frequency and interval (e.g., every 1 day, every 5 minutes). |
| **startTime**   | UTC datetime for trigger start. |
| **endTime**     | UTC datetime for trigger end. (Optional) |
| **timeZone**    | Time zone reference (e.g., `India Standard Time`). |
| **pipelines**   | Pipelines linked to the trigger. |

---

## 🔑 JSON Example (Daily Trigger)
```json
{
  "name": "DailyScheduleTrigger",
  "properties": {
    "type": "ScheduleTrigger",
    "typeProperties": {
      "recurrence": {
        "frequency": "Day",
        "interval": 1,
        "startTime": "2025-09-08T06:00:00Z",
        "endTime": "2025-12-31T23:59:00Z",
        "timeZone": "India Standard Time"
      }
    },
    "pipelines": [
      {
        "pipelineReference": {
          "referenceName": "Pipeline_DailyLoad",
          "type": "PipelineReference"
        }
      }
    ]
  }
}
````

---

## 🚀 Example Scenarios

### 1️⃣ Run Every Day at 6 AM

* Frequency → Day
* Interval → 1
* Start Time → 06:00:00

---

### 2️⃣ Run Every 15 Minutes

```json
"recurrence": {
  "frequency": "Minute",
  "interval": 15
}
```

---

### 3️⃣ Run Every Monday at 9 AM

```json
"recurrence": {
  "frequency": "Week",
  "interval": 1,
  "schedule": {
    "hours": [9],
    "minutes": [0],
    "weekDays": ["Monday"]
  }
}
```

---

## 📊 When to Use

* Daily ETL jobs.
* Weekly / Monthly reporting.
* Regular cleanup tasks.
* Scheduled ingestion from APIs or databases.

---

## 🎯 Key Takeaways

* **Schedule Trigger** is used for **time-driven automation** in ADF.
* Flexible scheduling with **intervals, time zones, and start/end times**.
* Ideal for **batch processing** but not suitable for **real-time events**.

---
