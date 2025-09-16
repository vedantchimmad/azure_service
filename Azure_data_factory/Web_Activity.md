# 🌐 Web Activity in Azure Data Factory (ADF)

---

## 📌 Introduction
The **Web Activity** in Azure Data Factory (ADF) is used to **call REST endpoints or custom web services** directly from a pipeline.  
It enables integration with **third-party APIs, Azure services, or custom applications**.

---

## ⚙️ Key Features
- Supports **GET, POST, PUT, DELETE** HTTP methods.  
- Allows passing **headers, query parameters, and request bodies**.  
- Can **authenticate** using Anonymous, Basic, Managed Identity, or Service Principal.  
- Returns **JSON response** that can be used in downstream activities.  
- Ideal for **triggering external processes or fetching metadata**.

---

## 🛠️ Properties

| Property         | Description |
|------------------|-------------|
| **URL**          | Endpoint to call (REST API/Service URL). |
| **Method**       | HTTP method (GET, POST, PUT, DELETE). |
| **Headers**      | Custom request headers (e.g., authorization, content-type). |
| **Body**         | Request body (for POST/PUT requests). |
| **Authentication** | Anonymous, Basic, MSI (Managed Identity), or Service Principal. |
| **Timeout**      | Maximum time before request fails. |

---

## 📊 Example 1: Simple GET Request
```json
{
  "name": "CallWeatherAPI",
  "type": "WebActivity",
  "typeProperties": {
    "url": "https://api.weather.com/v3/location?city=London",
    "method": "GET",
    "authentication": {
      "type": "Anonymous"
    }
  }
}
````

➡️ Calls weather API anonymously and fetches JSON response.

---

## 📊 Example 2: POST Request with Headers and Body

```json
{
  "name": "PostSalesData",
  "type": "WebActivity",
  "typeProperties": {
    "url": "https://api.company.com/sales/upload",
    "method": "POST",
    "headers": {
      "Content-Type": "application/json",
      "Authorization": "Bearer @{linkedService().accessToken}"
    },
    "body": {
      "date": "2025-09-12",
      "totalSales": 10500
    },
    "authentication": {
      "type": "Anonymous"
    }
  }
}
```

➡️ Posts sales data to an external REST API with JSON payload.

---

## 📊 Example 3: Calling API with Managed Identity

```json
{
  "name": "CallAzureFunction",
  "type": "WebActivity",
  "typeProperties": {
    "url": "https://myfunctionapp.azurewebsites.net/api/ProcessData",
    "method": "POST",
    "body": {
      "fileName": "sales_20250912.csv"
    },
    "authentication": {
      "type": "MSI",
      "resource": "https://management.azure.com/"
    }
  }
}
```

➡️ Securely calls an **Azure Function** using **Managed Identity**.

---

## 🚀 Workflow Example

**Scenario:** Trigger an external API after data load.

1. **Copy Activity** → Load file into Data Lake.
2. **Web Activity** → Notify downstream system via REST API.
3. **Stored Procedure Activity** → Update status in SQL DB.

Diagram:

```
Copy Data → Web Activity (Notify API) → Stored Procedure
```

---

## 🎯 Best Practices

* Use **Managed Identity** for secure API calls instead of storing credentials.
* Parse **JSON response** from API using **Lookup Activity** or pipeline variables.
* Always configure **timeout** to prevent pipeline hangs.
* Test API calls outside ADF (e.g., Postman) before implementing.

---

## 🏆 Key Takeaways

* **Web Activity** allows ADF to **call APIs and services**.
* Supports **GET/POST/PUT/DELETE** with authentication.
* Useful for **triggering external jobs, fetching metadata, or integrating with services**.
* Helps build **event-driven and service-integrated pipelines**.

---
