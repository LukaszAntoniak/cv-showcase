# ⚙️ Enterprise Middleware & ETL Suite

> **Note on Confidentiality:** This collection represents a series of "Headless" backend services developed under NDA. These systems function as the automated backbone for corporate audit, finance, and data synchronization workflows.

---

## 📋 Portfolio Overview
This suite consists of high-reliability **.NET 6 Worker Services**. These applications operate without an UI, focusing instead on complex data extraction (ETL), cross-system validation, and the elimination of manual administrative bottlenecks through robust background processing.

---

## 🛡️ 1. Automated Cloud Compliance & Audit Engine
**Context:** Developed to support the Internal Control Audit process for global cloud infrastructure.

* **The Challenge:** Manually auditing Azure security configurations across hundreds of resource groups is prone to human oversight, inconsistent reporting, and cannot be performed at the frequency required for modern compliance.
* **Description:** A headless .NET Worker Service that programmatically crawls cloud infrastructure via **Azure Resource Graph** and **Microsoft Graph API**. It evaluates resource states against corporate security baselines.
* **Key Achievement:** Transformed a multi-day manual audit cycle into a quick automated execution, providing 100% data coverage and removing human bias from the audit trail.

---

## 🧾 2. Intelligent Invoice & ERP Validation Service
**Context:** ERP Dispatch Auditor

* **The Challenge:** Due to intermittent synchronization issues, the ERP system frequently failed to generate and email invoices, especially during peak 'on-demand' request volumes. This forced the department team into a grueling manual audit—cross-referencing the "Demand List" against sent items in shared inboxes to identify missing dispatches.
* **The Solution:** Engineered an automated worker service to bridge the gap between the ERP and Microsoft 365. The service programmatically matched the ERP Demand Queue against real-time M365 Sent Folder metadata. It verified not only that an email was sent, but that it contained the correct PDF printout as a valid attachment.
* **Key Achievement:** Eliminated 100% of manual auditing labor and reduced the invoice-to-customer lifecycle. 

---

## 🧩 3. Dynamic JSON Ingestion & Storage Engine
**Context:** High-flexibility data ingestion from 3rd-party form and survey platforms with unstable schemas.

* **The Challenge:** External vendors frequently updated form structures and JSON schemas. In a traditional relational (SQL) environment, these changes caused frequent integration failures, requiring manual schema migrations and constant code redeployments.
* **Description:** Developed a schema-agnostic ingestion layer utilizing MongoDB as a flexible document store. The engine automatically adapts to incoming payload changes at runtime, ensuring seamless persistence of polymorphic JSON data. To maintain analytical consistency, Qlik Sense was leveraged to pull and flatten the raw document structures into structured reporting models.
* **Key Achievement:** Created a "Zero-Maintenance" pipeline that maintained **100% data continuity** despite frequent upstream changes from external providers.

---

## 📦 4. Core Enterprise Wrapper Libraries (The "Framework")
**Context:** A proprietary suite of NuGet-style DLLs built to standardize enterprise integration.

To maintain high code quality and accelerate development, I developed a collection of **Shared Enterprise Libraries** that encapsulate complex logic for the entire development team:

| Library | Technical Focus | Purpose |
| :--- | :--- | :--- |
| **SP-Bridge** | CSOM & Graph API | Unified wrapper for **SharePoint Online** and **Legacy 2013** environments. |
| **Qlik-Core** | WebSocket & REST | Encapsulates **Qlik Sense API** for automated reloads and metadata extraction. |
| **Auth-Master** | OAuth 2.0 / X.509 | Standardized **Entra ID (Azure AD)** and Certificate-based authentication. |
| **SQL-Common** | Dapper / EF Core | High-performance SQL wrappers with built-in audit logging and retry logic. |

---

## 🛠 Technical Commonalities (The "How")
Every service in this suite adheres to a strict "Production-Ready" standard:

* **Dockerized Deployment:** Every app is containerized, ensuring **Environment Parity** from local dev to production.
* **Secret Governance:** Zero hardcoded secrets; utilizing **Azure Key Vault** and Environment Variable injection.
* **Shared Observability:** Fully integrated with my **Custom NLog Library** for centralized telemetry.
* **Fault Tolerance:** Implemented **Polly** retry policies to ensure stability during transient network or API failures.

---
*Created for portfolio purposes. I am available to discuss the design patterns and the security-broker architecture utilized in these headless services during a technical interview.*