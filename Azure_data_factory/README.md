# ☁️ Azure Data Factory (ADF)

## 📌 What is ADF?
**Azure Data Factory** is a **cloud-based ETL (Extract, Transform, Load) and data integration service** provided by Microsoft Azure.  
It lets you create **data pipelines** to move and transform data across various sources at scale.

---

## 🧱 Key Components

| Component        | Description                                                            |
|------------------|------------------------------------------------------------------------|
| Pipeline         | A group of activities that perform a task                              |
| Activity         | An action like Copy Data, Execute SQL, or Data Flow                    |
| Dataset          | Metadata that points to input/output data sources                      |
| Linked Service   | Connection info for data sources (e.g., Azure Blob, SQL DB, etc.)       |
| Trigger          | Schedules or event-based starts for pipelines                          |
| Integration Runtime | Execution engine that runs your pipeline activities                  |

---

## 🔄 What Can ADF Do?

✅ Copy data from 100+ sources  
✅ Run transformations using **Mapping Data Flows** (code-free) or external compute (e.g., Databricks, HDInsight, SQL)  
✅ Schedule and orchestrate workflows  
✅ Monitor data pipelines with logs and alerts  
✅ Handle on-premise and cloud data with hybrid integration

---

## 📤 Example Use Case

🔹 **Copy data** from on-prem SQL Server to Azure Data Lake  
🔹 **Clean and transform** it using a Data Flow  
🔹 **Load it** into Azure Synapse Analytics for reporting

---

## 🛠️ Sample JSON Pipeline (Simplified)
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
