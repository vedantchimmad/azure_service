# 🔄 Pivot Transformation in Azure Data Factory (ADF) Data Flow

---

## 📌 Introduction
The **Pivot Transformation** in ADF Data Flow is used to **reshape data** by rotating rows into columns.  
It converts unique values from a column into multiple columns, similar to a **Pivot Table in Excel** or **SQL PIVOT**.

---

## ⚙️ Key Features
- Converts **row values into new columns**.  
- Groups data based on **one or more keys**.  
- Requires an **aggregate function** (e.g., SUM, COUNT, AVG, MIN, MAX).  
- Helps in **reporting and analytics** where data needs to be summarized.  

---

## 🛠️ Syntax (Conceptual)
```sql
SELECT 
    GroupByColumn,
    AggregateFunction(CASE WHEN PivotColumn = 'Value1' THEN DataColumn END) AS Value1,
    AggregateFunction(CASE WHEN PivotColumn = 'Value2' THEN DataColumn END) AS Value2
FROM Table
GROUP BY GroupByColumn;
````

---

## 🛠️ Configuring Pivot in ADF Data Flow

### 1️⃣ Group By

* Select the column(s) to **group rows**.
* Example: `Region`.

### 2️⃣ Pivot Key

* The column whose **unique values** become new column headers.
* Example: `Month`.

### 3️⃣ Aggregate Column

* The column whose values will be aggregated.
* Example: `SalesAmount`.

### 4️⃣ Aggregate Function

* The function to apply (SUM, COUNT, AVG, MIN, MAX).

---

## 📊 Example

### Input Data

| Region | Month | SalesAmount |
| ------ | ----- | ----------- |
| East   | Jan   | 100         |
| East   | Feb   | 150         |
| West   | Jan   | 200         |
| West   | Feb   | 250         |

---

### Pivot Configuration

* **Group By:** `Region`
* **Pivot Key:** `Month`
* **Aggregate Column:** `SalesAmount`
* **Function:** SUM

---

### Output Data

| Region | Jan | Feb |
| ------ | --- | --- |
| East   | 100 | 150 |
| West   | 200 | 250 |

---

## 🛠️ ADF UI Steps

1. Add a **Pivot Transformation** in your Data Flow.
2. Select **Group By column(s)** → e.g., `Region`.
3. Choose **Pivot Key** → e.g., `Month`.
4. Select **Aggregate column** → e.g., `SalesAmount`.
5. Choose an **Aggregate Function** (SUM/AVG/etc.).

---

## 📌 Use Cases

* Sales reporting (Months as columns).
* Survey data transformation.
* Converting transaction logs into summary tables.
* KPI dashboards requiring pivoted data.

---

## 🎯 Best Practices

* Ensure the **Pivot Key column** has limited distinct values (to avoid too many new columns).
* Use **derived column transformations** to clean data before pivoting.
* Combine with **Aggregate Transformation** for better summarization.
* Avoid pivoting very large datasets with too many distinct keys (can cause performance issues).

---

## 🏆 Key Takeaways

* Pivot Transformation reshapes rows into columns.
* Needs **Group By + Pivot Key + Aggregate Column + Function**.
* Output is **summarized, wide-format data**.
* Ideal for **analytics, reporting, and dashboards**.

---
