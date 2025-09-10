# 📘 Terms Used in Azure Data Factory (ADF)

---

## 📌 Introduction
Azure Data Factory (ADF) uses a set of **key concepts and terms** that define how data pipelines are built, executed, and monitored.  
Understanding these terms is essential for designing efficient **ETL/ELT workflows**.

---

## 🔑 Core Terms in ADF

| 🏷️ Term | 📖 Definition | 🎯 Purpose |
|---------|---------------|------------|
| **Pipeline** | A collection of **activities** that perform data movement and transformation. | Defines the **workflow** for data integration. |
| **Activity** | A single step within a pipeline (e.g., copy, execute stored procedure, run Databricks notebook). | Performs **specific actions** in the pipeline. |
| **Data Flow** | Visual, drag-and-drop interface to design **data transformation logic**. | Enables **code-free data transformation**. |
| **Linked Service** | Connection information (like connection strings) to external data sources/destinations. | Connects ADF with **data stores and compute services**. |
| **Dataset** | Metadata definition of data (e.g., table, file, folder). | Represents the **data structure** inside a linked service. |
| **Integration Runtime (IR)** | Compute infrastructure to run activities. | Executes **data movement and transformation**. |
| **Trigger** | Defines when and how pipelines are executed (schedule, event, tumbling window). | Automates **pipeline execution**. |
| **Control Flow** | Orchestration logic in pipelines (If, Switch, ForEach, Wait). | Adds **logic-based execution** inside pipelines. |
| **Mapping Data Flow** | ADF transformation component for ETL (join, aggregate, filter, etc.). | Enables **graphical transformations** without coding. |
| **Parameters** | Dynamic values passed into pipelines, datasets, or linked services. | Makes pipelines **flexible & reusable**. |
| **Variables** | Used to store values inside pipelines during execution. | Enables **state management** in workflows. |
| **Expressions** | Dynamic content expressions using ADF functions. | Allows **runtime calculations** (e.g., concat, substring). |
| **Control Activity** | Special activities like Execute Pipeline, If Condition, Until. | Provides **workflow control & orchestration**. |
| **Copy Activity** | Moves data from a source to a destination (ETL/ELT). | Core **data movement activity**. |
| **Monitoring** | ADF provides a monitoring dashboard for pipeline runs, activity status, and logs. | Helps track **success, failure, and performance**. |

---

## 🖥️ Types of Integration Runtime (IR)

| Type | Description | Use Case |
|------|-------------|----------|
| **Azure IR** | Fully managed compute in the cloud. | Cloud-to-cloud data movement. |
| **Self-Hosted IR** | Installed on-premises or VM. | On-prem to cloud data movement. |
| **SSIS IR** | Fully managed Azure-hosted SSIS execution environment. | Lift-and-shift existing SSIS packages. |

---

## 🕒 Trigger Types

| Trigger | Description | Example |
|---------|-------------|---------|
| **Schedule Trigger** | Runs pipelines on a schedule. | Daily at 9 AM. |
| **Tumbling Window Trigger** | Runs at regular intervals, processes data in fixed time windows. | Process hourly IoT data. |
| **Event-Based Trigger** | Runs when an event occurs (like file arrival in Blob storage). | Execute pipeline when new file is uploaded. |

---

## ⚡ Example Workflow (ADF Terms in Action)

1. Create a **Linked Service** to connect to Azure Blob Storage.  
2. Define a **Dataset** for a CSV file in Blob Storage.  
3. Build a **Pipeline** with a **Copy Activity** to move data to Azure SQL DB.  
4. Use **Parameters** for dynamic file paths.  
5. Schedule execution with a **Trigger**.  
6. Monitor pipeline in **ADF Monitoring** dashboard.  


