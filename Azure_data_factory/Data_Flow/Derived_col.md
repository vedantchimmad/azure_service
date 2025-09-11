# 🧮 Derived Column Transformation in Azure Data Factory (ADF) Data Flow

---

## 📌 Introduction
The **Derived Column transformation** in ADF Data Flow is used to **create new columns or modify existing columns** using expressions.  
It works like `ALTER TABLE ADD COLUMN` or `SELECT col1, col2, col1+col2 AS newCol` in SQL.

---

## ⚙️ Key Features
- Add **new calculated columns**.  
- Update/modify existing column values.  
- Apply **string, math, date, or conditional expressions**.  
- Supports **ADF expression language**.  
- Multiple derived columns can be created at once.  

---

## 🛠️ Properties
| Property       | Description |
|----------------|-------------|
| **Column name** | New or existing column to modify. |
| **Expression** | Formula or logic to generate values. |
| **Data type**  | Determined by expression result (string, int, date, etc.). |

---

## 🔑 Example Use Cases

### 1️⃣ Add a New Calculated Column
```text
New Column: FullName = FirstName + ' ' + LastName
````

---

### 2️⃣ Modify Existing Column

```text
Email → toLower(Email)
```

---

### 3️⃣ Apply Conditional Logic

```text
Status = iif(Age >= 18, 'Adult', 'Minor')
```

---

### 4️⃣ Date Transformation

```text
Year = year(OrderDate)
Month = month(OrderDate)
```

---

### 5️⃣ Numeric Calculation

```text
TotalPrice = Quantity * UnitPrice
DiscountedPrice = TotalPrice * 0.9
```

---

## 📊 Example Workflow

**Pipeline Goal:** Clean and enrich customer data.

1. **Source** → Customer dataset with raw fields.
2. **Derived Column** →

    * Create `FullName = FirstName + ' ' + LastName`.
    * Convert `Email` to lowercase.
    * Add `IsAdult = iif(Age >= 18, true, false)`.
3. **Sink** → Store enriched dataset in Synapse.

Diagram:

```
📂 Source (SQL: Customers)
      ↓
🧮 Derived Column (Add + Transform Fields)
      ↓
📊 Sink (Synapse: CustomersEnriched)
```

---

## 🚀 Example JSON Snippet

```json
{
  "name": "DerivedColumnTransformation",
  "type": "DerivedColumn",
  "typeProperties": {
    "columns": [
      { "name": "FullName", "expression": "concat(FirstName, ' ', LastName)" },
      { "name": "Email", "expression": "toLower(Email)" },
      { "name": "IsAdult", "expression": "iif(Age >= 18, true, false)" }
    ]
  }
}
```

---

## 🎯 Best Practices

* Use **meaningful column names** for new fields.
* Avoid recalculating the same expression multiple times — derive once, reuse later.
* Use **conditional logic** (`iif`, `case`) for flexible transformations.
* Validate **data types** (string, integer, date) to avoid errors.

---

## 🏆 Key Takeaways

* **Derived Column Transformation** = SQL `SELECT col1, col2, col1+col2 AS newCol`.
* Used to **add new fields or modify existing ones**.
* Supports **ADF expression language** for advanced logic.
* Essential for **data enrichment, cleaning, and feature engineering** in pipelines.

---
