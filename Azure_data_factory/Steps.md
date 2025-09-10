# 🛠️ Steps to Create an Azure Data Pipeline in ADF

---

## 📌 Introduction
An **Azure Data Pipeline** in **Azure Data Factory (ADF)** is a workflow that **moves and transforms data** between sources and destinations.  
The pipeline can be built using the **ADF Studio UI** or through **ARM templates / SDKs / CLI**.

---

## 🔑 Steps to Create a Data Pipeline

### 1️⃣ **Create an Azure Data Factory**
- Go to **Azure Portal** → Search for **Data Factory** → Click **Create**.
- Select:
  - **Subscription** (billing scope).
  - **Resource Group** (container for resources).
  - **Region**.
  - **Name** for Data Factory.
- Click **Review + Create** → Deploy.

---

### 2️⃣ **Open ADF Studio**
- After deployment, open **ADF Studio** (web-based UI).
- This is where you create pipelines, dataflows, and monitor activities.

---

### 3️⃣ **Create Linked Services**
- Go to **Manage → Linked Services**.
- Create connections to **data sources** (e.g., Azure Blob, SQL DB, Amazon S3, on-prem DB).
- Provide **authentication details** (keys, connection strings, service principals).

---

### 4️⃣ **Define Datasets**
- Go to **Author → Datasets**.
- Create **datasets** representing input (source) and output (sink) data.
  - Example: Blob CSV dataset, SQL table dataset.
- Each dataset is tied to a **Linked Service**.

---

### 5️⃣ **Build the Pipeline**
- Go to **Author → Pipelines** → **New Pipeline**.
- Add activities:
  - **Copy Activity** → Move data from source to sink.
  - **Data Flow** → Perform transformations (join, filter, aggregate).
  - **Control Activities** → (If Condition, ForEach, Execute Pipeline).
- Connect datasets to activities.

---

### 6️⃣ **Configure Parameters (Optional)**
- Define **pipeline parameters** for dynamic values (file paths, table names).
- Helps in **reusability and automation**.

---

### 7️⃣ **Set Triggers**
- Go to **Triggers** → Choose how the pipeline runs:
  - **Manual Run** → Trigger instantly.
  - **Schedule Trigger** → Run at fixed intervals (e.g., daily 9 AM).
  - **Tumbling Window Trigger** → Run in batch windows.
  - **Event Trigger** → Run when file arrives in Blob Storage.

---

### 8️⃣ **Publish Pipeline**
- Click **Publish All** to save changes.
- This makes the pipeline active and ready to run.

---

### 9️⃣ **Run & Monitor Pipeline**
- Trigger the pipeline manually or wait for scheduled execution.
- Go to **Monitor Tab**:
  - Track **pipeline runs**.
  - Check **success/failure** status.
  - Review **logs and performance metrics**.

---

## 📊 Pipeline Creation Workflow (Visual)

```

+-----------------+       +-------------------+       +-----------------+
|  Data Factory   | --->  |   Linked Services | --->  |     Datasets    |
+-----------------+       +-------------------+       +-----------------+
|
v
+-----------+
| Pipeline  |
| Activities|
+-----------+
|
v
+---------------+
|   Triggers    |
+---------------+
|
v
+----------------+
|   Monitoring   |
+----------------+

```

---

## 🚀 Example: Copy Data from Blob to SQL
1. Create a **Linked Service** for Blob & SQL DB.  
2. Create **Datasets** for Blob CSV file & SQL table.  
3. Create a **Pipeline** with a **Copy Activity**.  
4. Add a **Schedule Trigger** to run daily.  
5. **Publish & Monitor** execution.  

---

## 🎯 Key Takeaways
- ADF pipelines involve **Linked Services, Datasets, Pipelines, Activities, Triggers**.  
- Pipelines can be **scheduled, event-driven, or manual**.  
- Monitoring ensures **visibility and debugging**.  

---
