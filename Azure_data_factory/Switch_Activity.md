# 📝 Switch Activity in Azure Data Factory (ADF)

---

## 📌 Introduction
The **Switch Activity** in Azure Data Factory (ADF) is used to **implement branching logic** based on the value of an expression.  
It works similar to a **switch-case statement in programming languages**.  
This helps in building **dynamic pipelines** where different execution paths are chosen depending on conditions.

---

## ⚙️ Key Features
- Evaluates a given **expression**.  
- Routes execution to **one of multiple cases** that match the expression value.  
- Supports a **default case** if no match is found.  
- Helps avoid multiple **If Condition activities** when multiple branches are required.  

---

## 🛠️ Properties

| Property         | Description |
|------------------|-------------|
| **Expression**   | The expression to evaluate. |
| **Cases**        | Each case has a value and one or more activities to execute if matched. |
| **Default Case** | Activities executed when no case matches the expression. |

---

## 📊 Example 1: Simple Switch Case
```json
{
  "name": "SwitchActivityExample",
  "type": "Switch",
  "typeProperties": {
    "expression": "@pipeline().parameters.FileType",
    "cases": {
      "csv": {
        "activities": [
          { "name": "ProcessCSV", "type": "ExecutePipeline" }
        ]
      },
      "json": {
        "activities": [
          { "name": "ProcessJSON", "type": "ExecutePipeline" }
        ]
      }
    },
    "defaultActivities": [
      { "name": "ProcessOthers", "type": "ExecutePipeline" }
    ]
  }
}
````

➡️ If `FileType = "csv"`, it executes **ProcessCSV**.
➡️ If `FileType = "json"`, it executes **ProcessJSON**.
➡️ Otherwise, it executes **ProcessOthers**.

---

## 📊 Example 2: Dynamic Expressions in Switch

```json
{
  "name": "SwitchOnRegion",
  "type": "Switch",
  "typeProperties": {
    "expression": "@pipeline().parameters.Region",
    "cases": {
      "US": {
        "activities": [
          { "name": "USPipeline", "type": "ExecutePipeline" }
        ]
      },
      "EU": {
        "activities": [
          { "name": "EUPipeline", "type": "ExecutePipeline" }
        ]
      }
    },
    "defaultActivities": [
      { "name": "OtherRegionPipeline", "type": "ExecutePipeline" }
    ]
  }
}
```

➡️ Useful for **region-based processing**.

---

## 🚀 Workflow Example

**Scenario:** Process files differently based on file type.

1. **Get Metadata Activity** → Extracts file type.
2. **Switch Activity** → Routes pipeline based on `FileType`.
3. Executes the respective branch activity.

Diagram:

```
Get Metadata → Switch(FileType)
                 ├── csv  → ProcessCSV
                 ├── json → ProcessJSON
                 └── default → ProcessOthers
```

---

## 🎯 Best Practices

* Use **Switch Activity** instead of multiple nested If Conditions for clarity.
* Always configure a **default case** to handle unexpected values.
* Keep case values **simple and unique**.
* Use with **pipeline parameters** or **Lookup/Metadata outputs** for flexibility.

---

## 🏆 Key Takeaways

* **Switch Activity** provides branching logic like `switch-case`.
* Routes pipeline execution based on an **expression’s value**.
* Supports multiple cases and a **default case**.
* Best for **multi-path workflows** (e.g., by file type, region, or process type).

---
