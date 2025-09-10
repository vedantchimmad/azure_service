# 📘 Terms Used in Microsoft Azure Services

---

## 📌 Introduction
Microsoft **Azure** provides a wide range of services across compute, storage, networking, data, and security.  
Each service and resource in Azure is associated with specific **terminology** that helps in understanding how Azure works for **cloud computing and data engineering**.

---

## 🔑 Core Azure Terms

| 🏷️ Term | 📖 Definition | 🎯 Purpose |
|---------|---------------|------------|
| **Tenant ID** | A unique identifier for an Azure Active Directory (Azure AD) instance. | Represents the **root identity boundary** of an organization. |
| **Subscription** | A logical container that holds Azure resources and services. | Defines **billing scope and access control**. |
| **Resource Group** | A container that groups related resources (VMs, databases, storage). | Helps in **organizing and managing resources**. |
| **Resource** | An individual Azure service instance (VM, database, function, etc.). | The **building block** of Azure deployments. |
| **Region** | A geographical area where Azure data centers are located. | Defines where resources are physically hosted. |
| **Availability Zone (AZ)** | Independent data centers within a region. | Provides **high availability and fault tolerance**. |
| **Virtual Network (VNet)** | A private network for Azure resources. | Enables **network isolation and security**. |
| **VM (Virtual Machine)** | An IaaS compute service to run applications. | Provides **scalable computing power**. |
| **Azure AD (Active Directory)** | Identity and access management service. | Controls **authentication and authorization**. |
| **RBAC (Role-Based Access Control)** | Access management model in Azure. | Defines **permissions for users, groups, and apps**. |
| **Key Vault** | Service to store secrets, certificates, and encryption keys. | Provides **secure key and secret management**. |
| **Storage Account** | A container for Azure storage services (Blob, File, Queue, Table). | Central unit for **Azure storage resources**. |
| **Blob Storage** | Object storage for unstructured data (images, videos, logs). | Used for **data lakes and big data workloads**. |
| **Azure Monitor** | Monitoring service for logs, metrics, and alerts. | Provides **observability across resources**. |
| **Azure Resource Manager (ARM)** | Deployment and management layer in Azure. | Provides **templates and API-based automation**. |
| **ExpressRoute** | Private connection between on-premises and Azure. | Provides **secure hybrid connectivity**. |
| **Virtual Machine Scale Set (VMSS)** | Group of load-balanced VMs that scale automatically. | Used for **scalable workloads**. |
| **Azure Functions** | Serverless compute service. | Runs **event-driven applications**. |
| **App Service** | Managed platform for hosting web apps and APIs. | Provides **PaaS web application hosting**. |
| **Azure Synapse Analytics** | Cloud-based analytics and data warehouse service. | Used for **big data and analytics**. |
| **Cosmos DB** | Globally distributed NoSQL database. | Provides **low-latency, high-availability data storage**. |

---

## 🔐 Security & Identity Terms

| Term | Description | Purpose |
|------|-------------|---------|
| **Managed Identity** | Auto-managed identity for Azure services to access resources. | Removes need to manage secrets. |
| **Conditional Access** | Policy-based identity security in Azure AD. | Controls **who, when, and how users access resources**. |
| **Azure Policy** | Service for enforcing organizational rules and compliance. | Ensures **governance across resources**. |

---

## 🖥️ Compute & Networking Terms

| Term | Description | Purpose |
|------|-------------|---------|
| **AKS (Azure Kubernetes Service)** | Managed Kubernetes service. | Deploy and manage **containers at scale**. |
| **Load Balancer** | Distributes incoming traffic across resources. | Provides **scalability and redundancy**. |
| **Application Gateway** | Layer 7 load balancer with WAF. | Protects and routes web applications. |
| **NSG (Network Security Group)** | Firewall rules for VNets and subnets. | Controls **inbound/outbound traffic**. |

---

## 📊 Data & Integration Terms

| Term | Description | Purpose |
|------|-------------|---------|
| **ADF (Azure Data Factory)** | Cloud ETL and orchestration service. | Orchestrates **data pipelines**. |
| **Event Hubs** | Real-time event streaming service. | Ingests **big data streams**. |
| **Service Bus** | Enterprise-grade message broker. | Enables **queue-based communication**. |
| **Databricks on Azure** | Unified analytics platform. | Used for **big data, ML, and AI workloads**. |
| **Data Lake Storage (ADLS)** | Scalable data lake for analytics. | Stores **raw and curated datasets**. |

---

## 🎯 Key Takeaways
- Azure uses **Tenant → Subscription → Resource Group → Resource** hierarchy.  
- **Networking terms** like VNet, NSG, ExpressRoute are key for secure architecture.  
- **Identity terms** like Azure AD, RBAC, and Managed Identity ensure secure access.  
- **Data services** like ADF, Synapse, Event Hubs, and Blob Storage are core for **data engineering**.  

---
