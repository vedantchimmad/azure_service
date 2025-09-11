# 🔗 Join Transformation in Azure Data Factory (ADF) Data Flow

---

## 📌 Introduction
The **Join transformation** in ADF Data Flow is used to **combine two datasets** based on a **matching condition (key/column)**.  
It works similar to SQL `JOIN` operations and is widely used for **data enrichment, merging, and lookup operations**.

---

## ⚙️ Key Features
- Supports **all SQL-style joins** (Inner, Outer, Left, Right, Full, Cross).  
- Allows **multiple join conditions**.  
- Optimized for **big data processing** using Spark.  
- Can handle **null values** with special handling.  
- Useful for **fact-dimension joins** in data warehousing.  

---

## 🛠️ Types of Joins

| Join Type | Description | Example Use Case |
|-----------|-------------|------------------|
| **Inner Join** | Returns matching rows from both datasets. | Customers with matching orders. |
| **Left Outer Join** | All rows from left + matching rows from right. | All customers, with orders if available. |
| **Right Outer Join** | All rows from right + matching rows from left. | All orders, even if customer info is missing. |
| **Full Outer Join** | All rows from both datasets, match where possible. | Combine two sources with partial overlaps. |
| **Cross Join** | Cartesian product (every row with every row). | Useful in generating combinations. |
| **Self Join** | Join dataset with itself. | Employee-manager hierarchy. |

---

## 🔑 Syntax (Expression in ADF Data Flow)
```text
left.CustomerID == right.CustomerID
````

✅ Examples:

* `left.OrderID == right.OrderID`
* `toUpper(left.Region) == toUpper(right.Region)`
* `left.SalesDate >= right.StartDate && left.SalesDate <= right.EndDate`

---

## 🔧 Properties

| Property           | Description                        |
| ------------------ | ---------------------------------- |
| **Left Stream**    | First dataset in join.             |
| **Right Stream**   | Second dataset in join.            |
| **Join Condition** | Expression for matching rows.      |
| **Join Type**      | Type of join (inner, outer, etc.). |

---

## 🚀 Example Scenarios

### 1️⃣ Inner Join – Customers with Orders

```text
left.CustomerID == right.CustomerID
```

**Result:** Returns only customers who have placed orders.

---

### 2️⃣ Left Outer Join – All Customers, With or Without Orders

```text
left.CustomerID == right.CustomerID
```

**Result:** Includes all customers; if no orders exist → `NULL` in order columns.

---

### 3️⃣ Full Outer Join – Merge Two Datasets

```text
left.ProductID == right.ProductID
```

**Result:** Includes all products, regardless of whether they exist in both datasets.

---

### 4️⃣ Cross Join – Generate Combinations

No condition required.
**Result:** Every row in left dataset joins with every row in right dataset.

---

## 📊 Example Workflow

**Pipeline Goal:** Enrich Sales Data with Customer Information.

1. **Source 1** → `Customers` table.
2. **Source 2** → `Sales` table.
3. **Join Transformation** → Condition: `Customers.CustomerID == Sales.CustomerID`.
4. **Sink** → Write enriched dataset into Azure SQL Database.

Diagram:

```
📂 Customers ─┐
              ├── 🔗 Join (CustomerID)
📂 Sales    ──┘
              ↓
📊 Sink (SQL Database - EnrichedSales)
```

---

## 🎯 Best Practices

* **Filter data before joining** → reduces processing cost.
* Use **broadcast joins** when one dataset is small.
* Always **handle null values** in join conditions.
* Test joins with **debug mode** to validate expected output.

---

## 🏆 Key Takeaways

* **Join Transformation** = SQL `JOIN` in ADF Data Flow.
* Supports **Inner, Left, Right, Full, Cross, Self Joins**.
* Best for **data enrichment, merging, and fact-dimension lookups**.
* Optimize joins using **filtering, partitioning, and broadcast options**.

---
