# 📝 Wait Activity in Azure Data Factory (ADF)

---

## 📌 Introduction
The **Wait Activity** in Azure Data Factory is used to **pause pipeline execution for a specified duration** before continuing with the next activity.  
It is commonly used for **delays, retries, dependency waits, or scheduling adjustments** within pipelines.

---

## ⚙️ Key Features
- Suspends pipeline execution for a defined time period.  
- Accepts **static values** (fixed seconds) or **dynamic values** using expressions.  
- Useful in **event-driven pipelines** where a delay is needed before triggering next activity.  
- Can prevent **race conditions** (e.g., waiting for files or external processes).  

---

## 🛠️ Properties

| Property   | Description |
|------------|-------------|
| **Name**   | Activity name. |
| **Wait time in seconds** | Duration to pause execution (can be static or expression-based). |

---

## 📊 Example 1: Static Wait Time
```json
{
  "name": "Wait5Minutes",
  "type": "Wait",
  "typeProperties": {
    "waitTimeInSeconds": 300
  }
}
````

➡️ Pipeline execution pauses for **5 minutes**.

---

## 📊 Example 2: Dynamic Wait Time

```json
{
  "name": "DynamicWait",
  "type": "Wait",
  "typeProperties": {
    "waitTimeInSeconds": "@pipeline().parameters.DelaySeconds"
  }
}
```

➡️ Wait time is defined by a **pipeline parameter** (`DelaySeconds`).

---

## 📊 Example 3: Conditional Wait

```json
{
  "name": "ConditionalWait",
  "type": "Wait",
  "typeProperties": {
    "waitTimeInSeconds": "@if(equals(pipeline().parameters.IsWeekend, true), 86400, 60)"
  }
}
```

➡️ Waits **1 day (86400s)** if weekend, else waits **1 minute (60s)**.

---

## 🚀 Workflow Example

**Scenario:** A file lands in storage every hour, but downstream system needs 5 minutes buffer.

Pipeline steps:

1. **Trigger** (Hourly).
2. **Wait Activity** → 5 minutes.
3. **Copy Activity** → Load file into SQL DB.

Diagram:

```
Trigger → Wait (5 min) → Copy Data
```

---

## 🎯 Best Practices

* Avoid long wait times inside pipelines; consider **tumbling window or event triggers** instead.
* Use dynamic expressions for **flexibility** (e.g., environment-based delays).
* Keep wait durations **minimal** to reduce pipeline run costs.
* Use for **buffering time** when dealing with external dependencies.

---

## 🏆 Key Takeaways

* **Wait Activity** delays pipeline execution for a given duration.
* Supports both **static** and **dynamic** wait times.
* Useful for **buffering, retries, dependency handling, and scheduling**.
* Helps make pipelines **more controlled and reliable**.

---
