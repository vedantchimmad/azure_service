# 🔀 Union Transformation in Azure Data Factory (ADF) Data Flow

---

## 📌 Introduction
The **Union transformation** in Azure Data Factory (ADF) Data Flow is used to **combine rows from multiple datasets** into a single dataset.  
It works similar to **SQL UNION/UNION ALL**, allowing you to **merge data streams** for downstream processing.

---

## ⚙️ Key Features
- Merges **two or more input streams**.  
- Supports **schema alignment** (by name or by position).  
- Allows **duplicate rows** (works like `UNION ALL`).  
- Can handle **different column names** using **Select/Rename** before union.  

---

## 🛠️ Properties
| Property | Description |
|----------|-------------|
| **Input streams** | Two or more datasets to be combined. |
| **Union behavior** | ADF Union = SQL `UNION ALL` (keeps duplicates). |
| **Column mapping** | Columns must match (use `Select` to align). |

---

## 🔑 How It Works
1. Add multiple sources (e.g., `Source1`, `Source2`).  
2. Apply **Select** transformations (if needed) to align column names and datatypes.  
3. Use **Union** transformation to combine datasets.  
4. Pass result to **Sink** (e.g., SQL DB, Data Lake).  

---

## 🚀 Example Scenarios

### 1️⃣ Combine Sales Data from Two Regions
- **Input 1:** Sales from `Region_A`.  
- **Input 2:** Sales from `Region_B`.  
- **Union Output:** Combined sales dataset for reporting.  

---

### 2️⃣ Append Historical + Current Data
- **Input 1:** `Sales_History` (archived data).  
- **Input 2:** `Sales_Current` (new data).  
- **Union Output:** Full dataset with all sales.  

---

### 3️⃣ Merge Files from Different Folders
- **Input 1:** Blob folder `2025/Q1/`.  
- **Input 2:** Blob folder `2025/Q2/`.  
- **Union Output:** Combined dataset for year-to-date analysis.  

---

## 📊 Example Workflow
**Pipeline Goal:** Consolidate customer records from multiple systems.  

1. **Source 1** → Customers from SQL Database.  
2. **Source 2** → Customers from Blob Storage.  
3. **Select** → Rename/align columns.  
4. **Union** → Merge records into single dataset.  
5. **Sink** → Write consolidated customers into Azure Synapse.  

Diagram:
```

📂 Customers\_SQL ─┐
├── 🔀 Union
📂 Customers\_Blob ─┘
↓
📊 Sink (Synapse - UnifiedCustomers)

```

---

## ⚠️ Important Notes
- **ADF Union ≠ SQL UNION** → It behaves like **SQL UNION ALL** (keeps duplicates).  
- Use **Aggregate** or **Distinct** transformation if you need **unique rows**.  
- Ensure **schema consistency** across datasets.  

---

## 🎯 Best Practices
- Apply **Select** transformations before Union to align schema.  
- If datasets have large differences in size, ensure proper **partitioning**.  
- Use **Aggregate → Distinct** if deduplication is required.  
- Use **debug mode** to validate merged schema and data.  

---

## 🏆 Key Takeaways
- **Union Transformation** = SQL `UNION ALL`.  
- Combines multiple input streams into a single dataset.  
- Requires **schema alignment** (column names and types).  
- Ideal for **data consolidation, appending historical + new data, and merging regional data**.  

---

