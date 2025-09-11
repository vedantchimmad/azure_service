# 🔄 Data Flow in Azure Data Factory (ADF)

---

## 📌 Introduction
A **Data Flow** in Azure Data Factory (ADF) is a **visual data transformation tool** that allows you to design **ETL (Extract, Transform, Load)** processes at scale without writing complex code.  
It runs on **Azure Databricks under the hood**, providing **distributed data processing** with a drag-and-drop experience.  

---

## ⚙️ Key Features
- Code-free, **visual interface** for data transformations.  
- Runs on a **Spark cluster**, provisioned automatically by ADF.  
- Supports **batch** and **streaming data**.  
- Provides **debug mode** for testing transformations.  
- **Reusable and parameterized** components.  

---

## 🛠️ Types of Data Flows
1. **Mapping Data Flow**  
   - For **bulk data movement and transformation**.  
   - Example: Cleanse, join, and aggregate millions of records.  

2. **Wrangling Data Flow**  
   - Powered by **Power Query**.  
   - For **self-service, ad-hoc data preparation** by analysts.  

---

## 🏗️ Components of a Mapping Data Flow
| Component | Description |
|-----------|-------------|
| **Source** | Input dataset (e.g., Blob, ADLS, SQL, Cosmos DB). |
| **Transformations** | Business logic applied to data (e.g., join, filter, aggregate). |
| **Sink** | Destination dataset (e.g., Data Lake, Synapse, SQL Database). |

---

## 🔧 Common Transformations in Data Flow
| Transformation | Description |
|----------------|-------------|
| **Select** | Choose or rename columns. |
| **Filter** | Apply row-level conditions. |
| **Join** | Combine datasets (inner, outer, cross). |
| **Aggregate** | Perform group-based aggregations. |
| **Derived Column** | Add new calculated fields. |
| **Sort** | Order data by columns. |
| **Union** | Combine multiple datasets. |
| **Lookup** | Enrich data from reference datasets. |
| **Conditional Split** | Route data based on conditions. |
| **Window Functions** | Apply ranking, lag/lead, moving averages. |

---

## 🔑 Example Workflow
**Scenario:** Load and transform sales data from Blob → Apply transformations → Store in Azure SQL Database.

1. **Source** → Read `.csv` files from Blob Storage.  
2. **Filter** → Remove rows with null values.  
3. **Derived Column** → Create `Revenue = Price * Quantity`.  
4. **Aggregate** → Group by `Region` and calculate total revenue.  
5. **Sink** → Write results into Azure SQL Database.  

---

## 🖼️ High-Level Architecture (Design Icons)

```

📂 Source (Blob/ADLS/SQL)
↓
🔧 Transformations (Joins, Filters, Aggregates)
↓
📊 Sink (SQL DB / Synapse / Data Lake)

```

---

## 🚀 Execution Flow
1. Author Data Flow in ADF → Define transformations.  
2. ADF spins up a **Spark cluster** on-demand.  
3. Data processed in parallel across cluster nodes.  
4. Results written to the **Sink**.  

---

## 📊 When to Use Data Flows
- ETL/ELT pipelines at scale.  
- Data cleaning, enrichment, and aggregation.  
- Slowly Changing Dimensions (SCD) implementation.  
- Real-time analytics preparation.  

---

## 🎯 Key Takeaways
- **Mapping Data Flow** = Scalable ETL with Spark.  
- **Wrangling Data Flow** = Self-service data prep with Power Query.  
- Provides **drag-and-drop transformations** with **debugging support**.  
- Best for **large-scale data transformation** before loading into Data Lake, SQL, or Synapse.  

---
