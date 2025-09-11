# 🔍 Filter Transformation in Azure Data Factory (ADF) Data Flow

---

## 📌 Introduction
The **Filter transformation** in ADF Data Flow is used to **remove rows that do not meet specified conditions**.  
It works similarly to a `WHERE` clause in SQL — only records matching the filter expression are passed downstream.  

---

## ⚙️ Key Features
- Evaluates **row-level conditions** using **ADF expression language**.  
- Can reference **columns, functions, and parameters**.  
- Supports multiple logical operators (`AND`, `OR`, `NOT`).  
- Case-sensitive string comparisons (unless handled with functions).  

---

## 🛠️ Syntax (Expression Style)
```text
Condition: columnName operator value
````

✅ Examples:

* `Revenue > 1000`
* `Country == 'India'`
* `isNull(CustomerID) == false`
* `toLower(Region) == 'asia'`

---

## 🔧 Properties

| Property      | Description                              |
| ------------- | ---------------------------------------- |
| **Condition** | Expression that defines the filter rule. |
| **Output**    | Rows matching the condition.             |

---

## 🚀 Example Scenarios

### 1️⃣ Remove Null Values

```text
isNull(CustomerID) == false
```

### 2️⃣ Filter Sales Above Threshold

```text
Revenue > 5000
```

### 3️⃣ Select Customers from India or USA

```text
Country == 'India' || Country == 'USA'
```

### 4️⃣ Case-insensitive Match

```text
toLower(City) == 'bangalore'
```

---

## 📊 Example Workflow

**Pipeline Goal:** Load only high-value transactions into SQL Database.

1. **Source** → Sales data from Blob.
2. **Filter** → Condition: `Revenue > 10000`.
3. **Sink** → Write filtered records into Azure SQL Database.

Flow Diagram:

```
📂 Source (Sales.csv)
      ↓
🔍 Filter (Revenue > 10000)
      ↓
📊 Sink (SQL Database - HighValueSales)
```

---

## 🎯 Best Practices

* Always validate filter expressions in **debug mode**.
* Use **functions** (`toLower()`, `isNull()`, `substring()`) for complex conditions.
* Chain multiple conditions with **`AND`/`OR`** for flexibility.
* Apply filters **early in the flow** to reduce downstream processing.

---
## 🏆 Key Takeaways

* **Filter Transformation** = SQL `WHERE` clause in Data Flow.
* Helps in **row-level filtering** based on conditions.
* Supports **expressions, functions, and logical operators**.
* Improves performance by **reducing unnecessary data processing**.

---

