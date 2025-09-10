# 🕒 Tumbling Window Trigger in Azure Data Factory (ADF)

---

## 📌 Introduction
A **Tumbling Window Trigger** in Azure Data Factory (ADF) is a **time-based, recurring trigger** that divides time into **fixed-size, contiguous, and non-overlapping intervals (windows)**.  
Each window **triggers exactly once**, ensuring **deterministic and reliable execution**.  

It is best suited for **time-sliced data processing** like hourly or daily batch ingestion.

---

## ⚙️ Key Features
- **Fixed time intervals** (e.g., every hour, day).  
- **Exactly-once execution** per window.  
- Supports **backfilling** missed windows.  
- Supports **concurrent execution** of multiple windows.  
- Can set **dependencies between triggers**.  

---

## 🛠️ Properties
| Property              | Description |
|-----------------------|-------------|
| **frequency**         | Time unit (`Minute`, `Hour`, `Day`, `Week`, `Month`). |
| **interval**          | Interval between triggers (e.g., every 1 hour). |
| **startTime**         | UTC start time of the first window. |
| **endTime**           | UTC end time (optional). |
| **delay**             | Wait time before firing the trigger (to allow late data). |
| **maxConcurrency**    | Maximum number of concurrent pipeline runs. |
| **retryPolicy**       | Defines retry count and interval on failure. |
| **dependsOn**         | Allows chaining window dependencies. |

---

## 🔑 JSON Example (Hourly Trigger)
```json
{
  "name": "HourlyTumblingWindowTrigger",
  "properties": {
    "type": "TumblingWindowTrigger",
    "typeProperties": {
      "frequency": "Hour",
      "interval": 1,
      "startTime": "2025-09-08T00:00:00Z",
      "endTime": "2025-09-10T00:00:00Z",
      "maxConcurrency": 1,
      "delay": "00:05:00"
    },
    "pipelines": [
      {
        "pipelineReference": {
          "referenceName": "Pipeline_HourlyLoad",
          "type": "PipelineReference"
        }
      }
    ]
  }
}
````

---

## 🚀 Example Scenarios

### 1️⃣ Hourly Data Ingestion

* Frequency → Hour
* Interval → 1
* Load data for each hour (e.g., `2025-09-08 01:00 - 02:00`).

---

### 2️⃣ Daily Sales Processing

```json
"frequency": "Day",
"interval": 1,
"startTime": "2025-09-08T00:00:00Z"
```

---

### 3️⃣ Weekly Aggregation (Every Monday)

```json
"frequency": "Week",
"interval": 1,
"startTime": "2025-09-08T00:00:00Z"
```

---

## 📊 When to Use

* **Hourly or daily batch ingestion** from logs, APIs, or sensors.
* **Time-partitioned data processing** (e.g., process each day’s folder in Data Lake).
* **Backfilling missed windows** (re-run pipelines for past periods).
* **Data warehouse loads** (fact tables partitioned by time).

---

## 🎯 Key Takeaways

* **Tumbling Window Trigger** ensures **reliable, time-based execution**.
* Guarantees **exactly-once per window**.
* Supports **parallel runs, delay handling, and dependencies**.
* Best for **time-sliced batch processing** like hourly or daily ETL.

---
