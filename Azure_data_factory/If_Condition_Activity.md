# 🔀 If Condition Activity in Azure Data Factory (ADF)

---

## 📌 Introduction
The **If Condition Activity** in Azure Data Factory (ADF) allows you to execute activities **based on a Boolean expression**.  
It works like an **IF-ELSE statement in programming**, enabling **conditional branching** in pipelines.

---

## ⚙️ Key Features
- Evaluates an **expression** at runtime.  
- Executes activities in **True block** if condition evaluates to `true`.  
- Executes activities in **False block** if condition evaluates to `false`.  
- Supports ADF **system variables, parameters, functions, and activity outputs** in expressions.  

---

## 🛠️ Properties

| Property          | Description |
|-------------------|-------------|
| **Expression**    | The condition to evaluate (must return Boolean). |
| **IfTrueActivities**  | Activities executed if condition evaluates to `true`. |
| **IfFalseActivities** | Activities executed if condition evaluates to `false`. |

---

## 📊 Example 1: Check if File Exists

### Expression
```json
"expression": {
  "value": "@activity('GetMetadataFile').output.exists",
  "type": "Expression"
}
````

* If file exists → Execute Copy Activity.
* Else → Execute Set Variable Activity (log "File not found").

---

## 📊 Example 2: Compare Pipeline Parameter

### Expression

```json
"expression": {
  "value": "@equals(pipeline().parameters.env, 'prod')",
  "type": "Expression"
}
```

* If environment = `prod` → Load data into Production DB.
* Else → Load data into Dev DB.

---

## 📊 Example 3: Numeric Comparison

### Expression

```json
"expression": {
  "value": "@greater(pipeline().parameters.salesAmount, 1000)",
  "type": "Expression"
}
```

* If `salesAmount > 1000` → Run high-value process.
* Else → Run normal process.

---

## 🚀 Workflow Example

**Scenario:** Process daily sales file only if it exists.

1. **Get Metadata Activity** → Check `exists`.
2. **If Condition Activity**:

   * **True block:** Copy file to SQL.
   * **False block:** Log "No file available".

Diagram:

```
Get Metadata (exists?)
        ↓
     If Condition
   ┌──────────────┐
   │ True → Copy  │
   │ False → Log  │
   └──────────────┘
```

---

## 🎯 Best Practices

* Always validate **expressions return Boolean** (`true/false`).
* Use **system variables** (`@utcnow()`, `@pipeline().parameters`) for dynamic checks.
* For multiple conditions, combine with **AND/OR functions**:

  ```text
  @and(equals(pipeline().parameters.env,'prod'), greater(variables('rowCount'),0))
  ```
* Keep conditions simple for maintainability.
* Use **Switch Activity** if more than two branches are needed.

---

## 🏆 Key Takeaways

* **If Condition Activity** = Conditional branching in ADF.
* Executes **True block or False block** based on expression.
* Useful for **file checks, environment switches, and conditional data loads**.
* Expressions can use **parameters, variables, system variables, and activity outputs**.

---
