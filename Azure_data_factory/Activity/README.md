# ⚡ All Types of Activities in Azure Data Factory (ADF)

---

## 📌 Introduction
In **Azure Data Factory (ADF)**, activities define **tasks within a pipeline**.  
They are divided into **Data Activities, Transformation, Control Flow, and External/Integration**.  
Here’s the **full list including Copy, Move, Delete, and more**.

---

## 🔑 Categories of Activities

### 1️⃣ **Data Movement & Data Activities**
| Activity | Description | Example |
|----------|-------------|---------|
| **Copy Activity** | Copies data from a source to a sink. | Blob → Azure SQL DB |
| **Move Activity** | Copies data and then deletes from the source. | Blob → ADLS (remove from Blob after copy). |
| **Delete Activity** | Deletes data/files from a dataset. | Remove old CSVs from Blob storage. |
| **Get Metadata Activity** | Retrieves metadata of a dataset (size, modified date, structure). | Get file size before copy. |
| **Lookup Activity** | Retrieves rows from a dataset for downstream use. | Lookup SQL table values. |

---

### 2️⃣ **Data Transformation**
| Activity | Description | Example |
|----------|-------------|---------|
| **Mapping Data Flow** | Code-free data transformation. | Clean & join JSON + CSV. |
| **Wrangling Data Flow** | Power Query-based transformation. | Prep data for Power BI. |
| **Stored Procedure Activity** | Runs stored procedures in a DB. | Load data into SQL table. |
| **Databricks Notebook** | Executes Databricks notebooks. | Run PySpark jobs. |
| **Databricks Jar** | Runs a JAR on Databricks cluster. | Java ETL logic. |
| **Databricks Python** | Executes Python script in Databricks. | ML preprocessing. |
| **HDInsight Hive** | Runs Hive queries on HDInsight. | Query Hadoop data. |
| **HDInsight Pig** | Runs Pig scripts on HDInsight. | Transform logs. |
| **HDInsight MapReduce** | Runs MapReduce jobs. | Process JSON logs. |
| **HDInsight Spark** | Runs Spark jobs on HDInsight. | ETL & analytics. |
| **HDInsight Streaming** | Runs Hadoop streaming jobs. | Stream log processing. |
| **U-SQL Activity** | Executes U-SQL script in Data Lake Analytics (legacy). | Big data query. |

---

### 3️⃣ **Control Flow & Orchestration**
| Activity | Description | Example |
|----------|-------------|---------|
| **Execute Pipeline** | Calls another pipeline. | Modularized pipelines. |
| **ForEach** | Iterates over items in a collection. | Process multiple files. |
| **If Condition** | Runs activities conditionally. | If row count > 0. |
| **Switch** | Branches execution based on value. | Route by region. |
| **Until** | Loops until condition is true. | Retry until success. |
| **Wait** | Delays execution for a set duration. | Wait 10 minutes. |
| **Validation** | Validates dataset readiness. | Check if file exists. |

---

### 4️⃣ **External & Integration Activities**
| Activity | Description | Example |
|----------|-------------|---------|
| **Web Activity** | Calls REST APIs. | Trigger external service. |
| **Webhook Activity** | Calls API and waits for callback. | Notify workflow & wait. |
| **Custom Activity** | Executes custom code on Self-hosted IR. | Run Python/Java logic. |
| **Execute SSIS Package** | Runs SSIS packages in Azure SSIS IR. | Lift-and-shift ETL. |
| **Azure ML Execute Pipeline** | Runs Azure ML pipelines. | Retrain ML model. |
| **Azure ML Batch Execution** | Runs ML batch scoring. | Predict churn. |

---

## 📊 ADF Activity Classification Diagram

```
+-------------------------------------------------------------+
|                        ADF Activities                       |
+-------------------+---------------------+-------------------+
| Data Activities   | Data Transformation | Control Flow      |
| - Copy            | - Data Flows        | - Execute Pipe    |
| - Move            | - Stored Procedure  | - ForEach         |
| - Delete          | - Databricks Jobs   | - If / Switch     |
| - Get Metadata    | - HDInsight Jobs    | - Until / Wait    |
| - Lookup          | - U-SQL (Legacy)    | - Validation      |
+-------------------+---------------------+-------------------+
| External & Integration                                     |
| - Web / Webhook                                           |
| - Custom Activity                                          |
| - Execute SSIS Package                                     |
| - Azure ML (Pipeline / Batch)                             |
+-------------------------------------------------------------+

```

---

## 🚀 Example Hybrid Pipeline
1. **Get Metadata** → Check if file exists in Blob.  
2. **Copy Activity** → Copy file → ADLS.  
3. **Move Activity** → Move file → Archive folder.  
4. **Mapping Data Flow** → Clean & aggregate data.  
5. **Stored Procedure** → Load into Azure SQL DB.  
6. **If Condition** → Check data quality flag.  
7. **Databricks Notebook** → Train ML model.  
8. **Web Activity** → Notify completion to API.  

---

## 🎯 Key Takeaways
- **Data activities** include **Copy, Move, Delete, Get Metadata, Lookup**.  
- **Transformation activities** handle **ETL & ML workloads**.  
- **Control flow activities** add **orchestration & logic**.  
- **External activities** integrate APIs, SSIS, and ML pipelines.  

---
