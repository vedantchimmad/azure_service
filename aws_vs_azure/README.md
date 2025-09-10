## 🔑 Service Name Comparison

| Concept / Feature        | 🟡 **AWS Service**          | 🔵 **Azure Service**       | 📌 Notes |
|---------------------------|-----------------------------|-----------------------------|----------|
| **Identity Root**         | AWS **Account ID**          | Azure **Tenant ID**         | Tenant in Azure is like an AWS account root identity. |
| **Access Management**     | IAM **Group / Users / Roles** | Azure **Subscription / RBAC** | Subscription defines scope for billing & access, RBAC for permissions. |
| **Key Management**        | AWS **KMS (Key Management Service)** | Azure **Key Vault**        | Both manage keys, secrets, and encryption. |
| **Data Crawling**         | AWS **Glue Crawler**        | Azure **Integration Runtime** | AWS crawls metadata; Azure IR helps with ETL & data movement. |
| **Data Warehouse**        | Amazon **Redshift**         | Azure **Synapse Analytics** | Both are cloud-based data warehouses. |
| **Object Storage**        | Amazon **S3**               | Azure **Blob Storage / ADLS** | Both are scalable object storage. |
| **Queue Messaging**       | Amazon **SQS**              | Azure **Storage Queue / Service Bus** | Both enable async messaging. |
| **Event Streaming**       | Amazon **Kinesis**          | Azure **Event Hubs**        | Both used for real-time event ingestion. |
| **ETL / Orchestration**   | AWS **Glue**                | Azure **Data Factory (ADF)** | Both provide data pipeline orchestration. |
| **Serverless Compute**    | AWS **Lambda**              | Azure **Functions**         | Both are event-driven compute services. |
| **Monitoring**            | Amazon **CloudWatch**       | Azure **Monitor**           | Both provide monitoring & logging. |
| **Content Delivery**      | Amazon **CloudFront**       | Azure **Front Door / CDN**  | Both deliver content globally. |
| **Private Connectivity**  | AWS **Direct Connect**      | Azure **ExpressRoute**      | Both enable private cloud-to-on-prem links. |
| **Security & Governance** | AWS **IAM + Organizations** | Azure **Active Directory + Policy** | Both control security, identity & governance. |