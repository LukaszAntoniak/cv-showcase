# 🛠 Engineering Standards & Development Philosophy

> **Note on Confidentiality:** As a developer working on enterprise-grade systems, many of my core projects are protected by Non-Disclosure Agreements (NDAs). This document serves as a "Virtual Code Review," outlining the standards, architectural patterns, and security practices I apply to every project to ensure scalability, reliability, and clean maintainability.

---

## 🏗 1. Architectural Approach & System Design

My design process is rooted in high modularity and the strict separation of concerns, ensuring that complex integrations remain manageable.

* **Layered Service-Oriented Pattern:** I implement a robust **Controller / Service / Model** architecture. This is further extended by a dedicated **Infrastructure/External API** layer, isolating business logic from external interfaces like Qlik Sense, SharePoint, or Azure DevOps.
* **Middleware Orchestration:** My systems often function as intelligent "bridge" layers. They are designed to prepare "Commitment Feeds" and orchestrate external "Push" processes, providing a centralized control plane for decentralized data flows.
* **Domain Data Separation:** I maintain strict data integrity by separating **Data Models (DBModel)** from API models and **DTOs (Data Transfer Objects)**. This ensures that changes in a database schema or an external API do not ripple through the entire application logic.

---

## 🚀 2. Observability & Log-Driven Automation

Beyond basic error tracking, my approach focuses on Operational Intelligence. By transforming logs into actionable KPIs, the system can proactively mitigate potential downtime and system anomalies.

* **Centralized Telemetry:** Using a custom-built NLog shared library, all applications persist structured telemetry and critical activity logs into a centralized database for unified analysis.
* **BI Resource Monitor:** I developed a high-level tracking suite—the BI Resource Monitor—to aggregate cross-app activities, providing a "single pane of glass" to monitor health and performance across the entire web ecosystem.
* **Proactive Self-Healing:** The monitor is engineered to identify anomalies or predefined failure patterns in real-time, automatically triggering recovery scripts or notifications to resolve issues before they escalate into downtime.

---

## 🔒 3. Security & Identity Management

* **Service-to-Service Authentication:** I implement secure integrations via **Microsoft Entra ID (Azure AD) Service Principals**. By leveraging the **OAuth 2.0 Client Credentials flow**, I ensure that backend services communicate securely without user intervention.
* **Fine-Grained API Scopes:** I configure specific **API Permissions** within Azure Enterprise Applications, following the **Principle of Least Privilege** to ensure the orchestrator only accesses the data it absolutely needs.


---

## 🛠 Tech Stack Overview (Common Patterns)

* **Backend:** .NET 6 (Core), .NET Framework 4.x (Legacy Support)
* **Logging & Monitoring:** Custom NLog Shared Library, Database Persistence, BI Resource Monitor.
* **Integrations:** Qlik Engine/Repository API, SharePoint API (2013, online), Azure.
* **Identity:** Microsoft Entra ID (Enterprise Applications), OAuth 2.0, Kerberos/SSO Integration.
* **Infrastructure:** Docker (linux), IIS, SQL Server.


---
*Created for portfolio purposes. Contact me for a detailed walkthrough of the architectural decisions behind my projects.*