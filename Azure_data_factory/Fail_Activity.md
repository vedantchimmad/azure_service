# ❌ Fail Activity in Azure Data Factory (ADF)

---

## 📌 Introduction
The **Fail Activity** in Azure Data Factory (ADF) is used to **explicitly fail a pipeline** with a custom error message.  
It is useful when you want to **stop execution intentionally** if a condition is not met or an error scenario is detected.

---

## ⚙️ Key Features
- Allows setting a **custom error code** and **error message**.  
- Provides **clear visibility** into why the pipeline failed.  
- Can be combined with **If Condition, Switch, Lookup, or Validation activities** to enforce business rules.  
- Helps in **error handling, debugging, and validation checks**.  

---

## 🛠️ Properties

| Property       | Description |
|----------------|-------------|
| **Name**       | The activity name (identifier). |
| **Type**       | Must be `"Fail"`. |
| **Error Code** | Custom error code to display in pipeline run logs. |
| **Error Message** | Custom message explaining failure reason. |

---

## 📊 Example 1: Simple Fail Activity
```json
{
  "name": "FailPipeline",
  "type": "Fail",
  "typeProperties": {
    "errorCode": "CustomError001",
    "message": "Pipeline failed intentionally due to invalid input file."
  }
}
````

➡️ Pipeline execution **stops immediately** with the custom error code and message.

---

## 📊 Example 2: Conditional Fail with If Activity

```json
{
  "name": "CheckFileCondition",
  "type": "IfCondition",
  "typeProperties": {
    "expression": "@not(equals(pipeline().parameters.FileAvailable, true))",
    "ifTrueActivities": [
      {
        "name": "FailIfNoFile",
        "type": "Fail",
        "typeProperties": {
          "errorCode": "FileNotFoundError",
          "message": "The expected input file was not found. Pipeline stopped."
        }
      }
    ]
  }
}
```

➡️ If the input file is **not available**, the pipeline fails with a meaningful error message.

---

## 📊 Example 3: Fail After Validation

```json
{
  "name": "ValidateData",
  "type": "IfCondition",
  "typeProperties": {
    "expression": "@greater(activity('RowCountCheck').output.firstRow.Count, 0)",
    "ifFalseActivities": [
      {
        "name": "FailDueToEmptyData",
        "type": "Fail",
        "typeProperties": {
          "errorCode": "NoDataError",
          "message": "Validation failed. The dataset is empty."
        }
      }
    ]
  }
}
```

➡️ If dataset is **empty**, pipeline execution stops with a **NoDataError**.

---

## 🚀 Workflow Example

**Scenario:** Stop pipeline if input file is missing.

1. **Validation Activity** → Check if file exists.
2. **If Condition** → If file missing, run Fail Activity.
3. **Fail Activity** → Stop pipeline with error message.

Diagram:

```
Validation → If Condition → Fail Activity
```

---

## 🎯 Best Practices

* Use **Fail Activity with custom error codes** for better observability.
* Place it after **validation checks** or **business rules**.
* Helps in debugging by providing **clear failure reasons** in pipeline logs.
* Avoid using generic failure messages; always give **specific context**.

---

## 🏆 Key Takeaways

* **Fail Activity** explicitly stops pipeline execution.
* Provides **custom error codes and messages**.
* Useful for **business rule enforcement, debugging, and error handling**.
* Ensures pipelines fail **intentionally with clarity** rather than unexpected errors.

---
