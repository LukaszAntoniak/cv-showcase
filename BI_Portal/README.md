# BI Portal Hub

> **Note on Confidentiality:** This project is a proprietary commercial application developed under a Non-Disclosure Agreement (NDA). To respect intellectual property rights, the source code is not publicly available. This documentation serves as a functional and architectural case study.

---

## 💼 Business Context: BI Portal Hub & Service Orchestration
The BI Portal Hub acts as a centralized Service Catalog and Orchestration Engine for the organization's business intelligence landscape. It consolidates application discovery, user access management, and deployment workflows into a single interface.

* **Application Discovery & Inventory:** Served as the authoritative source of truth for the organization’s BI ecosystem, providing a comprehensive, searchable inventory of all internally developed BI applications and assets.

* **Granular Access Management:** Automates the lifecycle of user permissions for Qlik Sense platform. The portal implements a dimension-based access model, allowing administrators to provision end-user rights dynamically based on organizational attributes, ensuring data security and compliance.

* **Automated Environment Promotion:** Replaces manual DevOps tasks with a fully automated CI/CD pipeline for Qlik Sense applications. The system orchestrates the promotion of BI assets between testing and production environments, significantly reducing deployment latency.

* **Workflow Automation:** Provides a dedicated request interface for BI activities, tracking the status of deployments and administrative tasks through a structured, audit-ready workflow.


---

## 🛠️ Tech Stack & Skills
* **Backend:** .NET Framework (IIS App Pool).
* **Frontend:** React (SPA), MSAL.js, HashRouter, Static Assets Deployment.
* **Identity & Security:** OAuth2 / OpenID Connect (OIDC), MS Entra ID (B2B), Custom Token Management Service, CORS Policy Management, IIS URL Rewrite (Gateway Pattern).
* **Infrastructure:** IIS (Internet Information Services), Windows Server 2019.
* **Database:** MS SQL Server 2016 (Bare-Metal).

---

## 🧠 Key Decisions & "Why"
* **Strategic .NET Framework Implementation:** Opted for a native IIS-hosted .NET Framework deployment rather than containerization. 
  * *Why:* The application relies heavily on specific legacy Windows Server OS integrations and deep-level IIS bindings required for seamless Qlik Sense interoperability. Hosting natively within IIS App Pools provides the highest performance and stability for these specific dependencies without the unnecessary abstraction overhead of a container layer.
* **Bare-Metal SQL Server Strategy:** Leveraged Docker to standardize developer environments.
  * *Why:* Maximizes performance by eliminating ORM overhead, allowing for full control over execution plans for complex, dimension-heavy BI data processing.
* **Custom OIDC Token Flow:** Implemented a proprietary MSAL-based token management service.
  * *Why:* Provides a secure bridge between MS Entra ID (external identity) and internal RBAC, enabling granular access control linked directly to BI analytics data.
* **IIS as Reverse Proxy & SSL Termination:** Offloaded traffic orchestration and SSL management to the IIS layer.
  * *Why:* Ensures centralized CORS policy enforcement, better security compliance, and cleaner container configuration.
* **Custom OIDC Token Flow:** Implemented a proprietary MSAL-based token management service.
  * *Why:* Provides a secure bridge between MS Entra ID (external identity) and internal RBAC, enabling complex role-based access control linked directly to BI analytics data.

---

*Created for portfolio purposes. Contact me for a detailed walkthrough of the architectural decisions behind this project.*