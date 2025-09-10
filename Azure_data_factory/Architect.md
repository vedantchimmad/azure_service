# 🏗️ Azure Data Factory (ADF) Architecture

---

## 📌 Introduction
**Azure Data Factory (ADF)** is a **cloud-based ETL and data integration service** that allows you to create, schedule, and orchestrate **data pipelines**.  
It is designed to move data from **multiple sources** to **target systems** (on-premises or cloud) for **analytics and reporting**.

---

## 🔑 Core Components of ADF Architecture

### 1. 📂 **Pipelines**
- Logical grouping of **activities** that perform data movement and transformation.  
- Example: Copy data from Azure Blob Storage → Transform in Databricks → Load into Azure SQL.

---

### 2. ⚡ **Activities**
- Tasks that define what to do inside a pipeline.  
- Types:
  - **Data Movement** → Copy activity.  
  - **Data Transformation** → Data Flow, Databricks, HDInsight, SQL activities.  
  - **Control** → If Condition, ForEach, Wait, Execute Pipeline.  

---

### 3. 🔌 **Linked Services**
- Connection strings and credentials to connect ADF with **data sources & destinations**.  
- Example: Linked service to Azure SQL DB or Amazon S3.  

---

### 4. 🗄️ **Datasets**
- Represent **data structures** (tables, files, folders) inside linked services.  
- Example: A dataset representing a CSV file in Blob Storage.  

---

### 5. 🌐 **Integration Runtime (IR)**
- Compute infrastructure used by ADF to execute activities.  
- Types:
  - **Azure IR** → Executes activities in Azure (default).  
  - **Self-hosted IR** → For on-premises or private network data sources.  
  - **SSIS IR** → Lift-and-shift of existing SSIS packages.  

---

### 6. 🕒 **Triggers**
- Define **pipeline execution schedule** or event-based execution.  
- Types:
  - **Schedule Trigger** → Runs at defined intervals.  
  - **Tumbling Window Trigger** → Processes data in time-based chunks.  
  - **Event-based Trigger** → Executes on file arrival or blob events.  

---

### 7. 📊 **Monitoring**
- Real-time monitoring and alerts for pipeline runs.  
- Integration with **Azure Monitor & Log Analytics**.  

---

## 🔄 ADF Workflow

1. 📝 Define **Pipelines** with **Activities**.  
2. 🔌 Connect data using **Linked Services**.  
3. 🗂️ Define input/output **Datasets**.  
4. ⚡ Execute activities using **Integration Runtime**.  
5. 🕒 Schedule execution using **Triggers**.  
6. 📊 Monitor and manage pipeline runs.  

---

## 📊 Azure Data Factory Architecture Diagram (Conceptual)

```
               +-----------------------------+
               |        Data Sources         |
               | (On-Prem, Cloud, SaaS Apps) |
               +--------------+--------------+
                              |
                              v
                    +-------------------+
                    |   Linked Services |
                    +-------------------+
                              |
                              v
               +--------------------------------+
               |         Pipelines              |
               |   (Activities + Data Flows)    |
               +--------------------------------+
                              |
                              v
                +------------------------------+
                |  Integration Runtime (IR)    |
                | Azure IR | Self-hosted | SSIS|
                +------------------------------+
                              |
                              v
               +-------------------------------+
               |       Data Destinations       |
               | (ADLS, Blob, SQL, Synapse, BI)|
               +-------------------------------+
```
---

## 🚀 Example: Copy Data Pipeline (ADF JSON)

```json
{
  "name": "CopyBlobToSQL",
  "properties": {
    "activities": [
      {
        "name": "CopyFromBlobToSQL",
        "type": "Copy",
        "inputs": [ { "referenceName": "BlobDataset", "type": "DatasetReference" } ],
        "outputs": [ { "referenceName": "SQLDataset", "type": "DatasetReference" } ],
        "typeProperties": {
          "source": { "type": "BlobSource" },
          "sink": { "type": "SqlSink" }
        }
      }
    ]
  }
}
````

---

## 🎯 Key Highlights

* ADF = **Orchestration + ETL + Data Integration**.
* Uses **Pipelines, Activities, Linked Services, Datasets, Triggers**.
* **Integration Runtime** is the execution engine.
* Supports **hybrid data movement** (cloud + on-prem).
* Built-in **monitoring** with alerts.

---