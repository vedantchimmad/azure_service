# 📦 Copy Activity in Azure Data Factory (ADF)

---

## 📌 Introduction
The **Copy Activity** is one of the most commonly used activities in **Azure Data Factory (ADF)**.  
It is designed to **copy data from a source (input dataset) to a destination (output dataset)**.  
It supports a wide range of **data stores** such as **Azure Blob, Data Lake, SQL, Cosmos DB, On-premises DBs, SaaS apps, and REST APIs**.

---

## ⚙️ How It Works
1. **Connects to a Source** → Reads data from the input dataset.  
2. **Performs Serialization/Deserialization** → Converts data into required format (CSV, JSON, Parquet, Avro, ORC, etc.).  
3. **Writes to Sink** → Loads the data into the target store.  

---

## 🛠️ Syntax (JSON Pipeline Definition Example)
```json
{
  "name": "CopyFromBlobToSQL",
  "properties": {
    "activities": [
      {
        "name": "CopyBlobToSQL",
        "type": "Copy",
        "inputs": [
          { "referenceName": "BlobDataset", "type": "DatasetReference" }
        ],
        "outputs": [
          { "referenceName": "SQLDataset", "type": "DatasetReference" }
        ],
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

## 🔑 Key Components

| Component                    | Description                                                  |
| ---------------------------- | ------------------------------------------------------------ |
| **Source**                   | Defines the input dataset (e.g., Blob, SQL, REST API).       |
| **Sink**                     | Defines the output dataset (e.g., SQL, ADLS, Synapse).       |
| **Integration Runtime (IR)** | Compute used for data movement (Azure IR or Self-hosted IR). |
| **Mapping**                  | Maps source schema to sink schema (optional).                |
| **Performance Settings**     | Batch size, parallelism, fault tolerance.                    |

---

## ⚡ Supported Source & Sink Types

* **File-based**: Blob, ADLS, FTP, SFTP, Amazon S3, Google Cloud Storage.
* **Databases**: Azure SQL, SQL Server, MySQL, PostgreSQL, Oracle, Snowflake.
* **NoSQL**: Cosmos DB, MongoDB, Cassandra.
* **SaaS Apps**: Salesforce, Dynamics 365, ServiceNow, SAP.
* **REST & OData APIs**.

---

## 🚀 Example: Copy CSV from Blob → Azure SQL Database

### 1️⃣ Create Linked Services

* **Azure Blob Storage** (source).
* **Azure SQL Database** (sink).

### 2️⃣ Create Datasets

* Input: Blob (CSV).
* Output: Azure SQL table.

### 3️⃣ Pipeline with Copy Activity

```json
{
  "name": "BlobToSQLPipeline",
  "properties": {
    "activities": [
      {
        "name": "CopyBlobToSQL",
        "type": "Copy",
        "inputs": [
          { "referenceName": "BlobDataset", "type": "DatasetReference" }
        ],
        "outputs": [
          { "referenceName": "SQLDataset", "type": "DatasetReference" }
        ],
        "typeProperties": {
          "source": { "type": "DelimitedTextSource" },
          "sink": { "type": "SqlSink" },
          "enableStaging": false
        }
      }
    ]
  }
}
```

---

## 📊 Performance Optimization

* Enable **parallel copy** for large datasets.
* Use **staging copy** with Azure Blob or ADLS for transformations.
* Configure **fault tolerance** (skip incompatible rows, log errors).
* Tune **batch size** and **max concurrent connections**.

---

## 🎯 Key Takeaways

* **Copy Activity** is the foundation of ETL pipelines in ADF.
* Supports **100+ data sources and sinks**.
* Handles **schema mapping, format conversion, fault tolerance, and performance tuning**.
* Can be used with **triggers** for **batch or real-time ingestion**.

---
