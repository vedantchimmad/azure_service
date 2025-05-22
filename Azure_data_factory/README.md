# ☁️ Azure Data Factory (ADF)

###  📌 What is ADF?
**Azure Data Factory** is a **cloud-based ETL (Extract, Transform, Load) and data integration service** provided by Microsoft Azure.  
It lets you create **data pipelines** to move and transform data across various sources at scale.

---

### 🧱 Key Components

| Component        | Description                                                            |
|------------------|------------------------------------------------------------------------|
| Pipeline         | A group of activities that perform a task                              |
| Activity         | An action like Copy Data, Execute SQL, or Data Flow                    |
| Dataset          | Metadata that points to input/output data sources                      |
| Linked Service   | Connection info for data sources (e.g., Azure Blob, SQL DB, etc.)       |
| Trigger          | Schedules or event-based starts for pipelines                          |
| Integration Runtime | Execution engine that runs your pipeline activities                  |

---

### 🔄 What Can ADF Do?

✅ Copy data from 100+ sources  
✅ Run transformations using **Mapping Data Flows** (code-free) or external compute (e.g., Databricks, HDInsight, SQL)  
✅ Schedule and orchestrate workflows  
✅ Monitor data pipelines with logs and alerts  
✅ Handle on-premise and cloud data with hybrid integration

---

### 📤 Example Use Case

🔹 **Copy data** from on-prem SQL Server to Azure Data Lake  
🔹 **Clean and transform** it using a Data Flow  
🔹 **Load it** into Azure Synapse Analytics for reporting

---

### 🛠️ Sample JSON Pipeline (Simplified)
```json
{
  "name": "CopySalesDataPipeline",
  "properties": {
    "activities": [
      {
        "name": "CopyFromBlobToSQL",
        "type": "Copy",
        "inputs": [{ "referenceName": "BlobSalesData" }],
        "outputs": [{ "referenceName": "SQLSalesTable" }],
        "typeProperties": {
          "source": { "type": "DelimitedTextSource" },
          "sink": { "type": "SqlSink" }
        }
      }
    ]
  }
}
```

### 🧩 Azure Data Factory (ADF) – Core Components

Azure Data Factory is a cloud-based data integration service that allows you to create, schedule, and orchestrate data pipelines.

### 🧱 1. Pipeline

* A **pipeline** is a container for one or more activities.



* A pipeline is a **logical container** for a sequence of activities.

```json
{
  "name": "MyDataPipeline",
  "properties": {
    "activities": []
  }
}
```

---

### 🏗 2. Activity

An **activity** is a single task, such as copying data or executing a SQL script.

**Common activity types**:
- `CopyActivity`
- `DataFlowActivity`
- `ExecutePipelineActivity`
- `NotebookActivity`
```json
{
  "name": "CopyBlobToSQL",
  "type": "Copy",
  "inputs": ["BlobInput"],
  "outputs": ["SqlOutput"],
  "typeProperties": {
    "source": { "type": "DelimitedTextSource" },
    "sink": { "type": "SqlSink" }
  }
}
```

---

### 📁 3. Dataset

* A **dataset** represents input or output data — like a file or table.
* A dataset defines **metadata** pointing to the data you want to use.

```json
{
  "name": "BlobSalesData",
  "type": "Dataset",
  "properties": {
    "linkedServiceName": { "referenceName": "AzureBlobStorage" },
    "type": "DelimitedText",
    "typeProperties": {
      "location": { "type": "AzureBlobStorageLocation", "folderPath": "raw/sales" },
      "columnDelimiter": ",",
      "firstRowAsHeader": true
    }
  }
}
```

---

### 🔗 4. Linked Service

A **linked service** defines the connection to a data source or compute resource.

```json
{
  "name": "AzureSQLLinkedService",
  "type": "LinkedService",
  "properties": {
    "type": "AzureSqlDatabase",
    "typeProperties": {
      "connectionString": "Server=tcp:myserver.database.windows.net;Database=mydb;..."
    }
  }
}
```

---

### ⏰ 5. Trigger

* A **trigger** defines when a pipeline is executed.
* A trigger defines **when and how** a pipeline should execute.


⏱ **Types**:
- **Schedule Trigger** : Runs pipelines at **specific intervals** (e.g., hourly, daily).
- **Tumbling Window** : Processes data in **fixed-size, non-overlapping intervals**. Supports **retry, concurrency, and dependency** chaining.
- **Event Trigger** : Triggers a pipeline based on **blob creation or deletion events** in Azure Storage.
- **Manual Trigger** : Pipelines can be executed manually **without a defined trigger**

| Feature                     | Schedule Trigger        | Tumbling Window Trigger             |
|-----------------------------|-------------------------|-------------------------------------|
| Time Window Overlap         | Can overlap             | Fixed, non-overlapping              |
| Dependency Support          | ❌ No                    | ✅ Yes                               |
| Backfill Support            | ❌ No                    | ✅ Yes                               |
| Retry on Failure            | ❌ No                    | ✅ Yes                               |
| Runs if Previous Fails?     | ✅ Yes                   | ❌ No (unless retried/backfilled)    |
| Use Case                    | Simple recurring tasks  | Time-partitioned ingestion          |

```json
{
  "name": "DailyTrigger",
  "type": "ScheduleTrigger",
  "properties": {
    "recurrence": {
      "frequency": "Day",
      "interval": 1
    }
  }
}
```

---

### 🖥️ 6. Integration Runtime (IR)

IR is the **compute environment** for running activities.

### Types:
- `Azure` (default for cloud)
- `Self-hosted` (on-premise)
- `Azure-SSIS` (for SSIS packages)

```json
{
  "name": "AzureIR",
  "type": "IntegrationRuntimeReference",
  "referenceName": "AutoResolveIntegrationRuntime"
}
```

---

### 🧮 7. Parameters

**Parameters** allow pipelines and datasets to be dynamic.

```json
"parameters": {
  "filename": {
    "type": "String"
  }
}
```

---

### 🔄 8. Data Flow

* **Data Flows** provide visual, drag-and-drop transformation capabilities.
* A **Data Flow** is a **graphical data transformation** component in ADF

### 🔄 Common Transformations

| Transformation    | Purpose                                  |
|-------------------|------------------------------------------|
| Filter            | Include/exclude rows based on conditions |
| Join              | Combine data from two sources            |
| Derived Column    | Create new columns using expressions     |
| Aggregate         | Perform groupings and aggregations       |
| Conditional Split | Route data to different paths            |
| Pivot/Unpivot     | Reshape tabular data                     |
| Surrogate Key     | Add unique identifiers                   |
| Lookup            | Reference data from another source       |

```json
{
  "name": "CleanSalesDataFlow",
  "type": "MappingDataFlow",
  "typeProperties": {
    "sources": [...],
    "transformations": [...],
    "sinks": [...]
  }
}
```

---

### 📊 Summary Table

| Component           | Purpose                                 |
|---------------------|------------------------------------------|
| Pipeline            | Container of activities                  |
| Activity            | Task like Copy, Lookup, Execute Notebook |
| Dataset             | Input/output data descriptor             |
| Linked Service      | Data source connection                   |
| Trigger             | Defines execution schedule               |
| Integration Runtime | Compute engine for pipeline execution    |
| Parameters          | Makes logic dynamic and reusable         |
| Data Flow           | GUI-based data transformation logic      |

---


