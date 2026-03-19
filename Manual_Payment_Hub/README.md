# Manual Payment Hub 

> **Note on Confidentiality:** This project is a proprietary commercial application developed under a Non-Disclosure Agreement (NDA). To respect intellectual property rights, the source code is not publicly available. This documentation serves as a functional and architectural case study.

---

## 🛡️ Financial Governance & Business Context
This module acts as a secure "Data Integrity Guard" between ERP and external banking payment system, ensuring that all manually initiated payment records are compliant with internal financial controls.

* **Policy Enforcement Engine:** Mandates strict adherence to internal security frameworks for all manual payment requests, replacing fragmented processes with a centralized, system-enforced workflow.
* **Hierarchical Approval Flow:** Implements a multi-level approval matrix, routing requests up to executive authorization levels based on the Delegation of Authorities (DoA) matrix.
* **Data Integrity Guard:** Acts as a gatekeeper for payment data, performing real-time validation against authorized master records to ensure accuracy and prevent fraud.
* **Third-Party Integration:** Securely exports validated data to external banking platforms via controlled CSV pipelines, ensuring that only approved, high-integrity transactions reach the execution stage.
* **Audit & Traceability:** Generates an immutable audit trail for every request, change, and approval action, ensuring full transparency for financial audits.

---

## 🛠️ Tech Stack & Skills
* **Backend:** .NET 6 (Containerized), ASP.NET Core API.
* **Frontend:** React (SPA), MSAL.js, HashRouter, Static Assets Deployment.
* **Identity & Security:** OAuth2 / OpenID Connect (OIDC), MS Entra ID (B2B), Custom Token Management Service, CORS Policy Management.
* **Infrastructure:** IIS, URL Rewrite Module, Docker, Windows Server 2019.
* **Database:** MS SQL Server 2016 (Bare-Metal).

---

## 🧠 Key Decisions & "Why"
* **Segmented Containerization:** To minimize resource overhead, legacy modules remain in dedicated IIS App Pools, while core management services are deployed as lightweight .NET 6 containers. 
  * *Why:* Provides a path for modernization without requiring a full system rewrite, while keeping the core API isolated and portable.
* **IIS as Reverse Proxy & SSL Termination:** Offloaded traffic orchestration and SSL management to the IIS layer.
  * *Why:* Ensures centralized CORS policy enforcement, better security compliance, and cleaner container configuration.
* **Bare-Metal SQL Server Strategy:** Opted for a direct, abstraction-free database connection.
  * *Why:* Maximizes performance by eliminating ORM overhead, allowing for full control over execution plans for high-volume BI data processing.
* **Custom OIDC Token Flow:** Implemented a proprietary MSAL-based token management service.
  * *Why:* Provides a secure bridge between MS Entra ID (external identity) and internal RBAC, enabling complex role-based access control linked directly to BI analytics data.

---

## 🚀 Key Achievements (Impact)

### 1. Dockerization & Environment Parity
Created a multi-stage `Dockerfile` for the core API, which reduced the "onboarding" time for new developers from days to minutes.
> **Outcome:** Eliminated deployment inconsistencies by encapsulating the runtime environment, ensuring the API behaves identically across dev and production.

### 2. Performance Tuning & Stability
Optimized IIS Application Pool recycling policies and memory limits to accommodate both legacy modules and containerized API services.
> **Outcome:** Achieved 99.9% uptime during peak transaction hours, preventing memory issues in legacy components from impacting the core API.

### 3. CI/CD Modernization
Transitioned from manual, high-risk file deployments to an automated, image-based workflow.
> **Outcome:** Reduced deployment downtime by 70% using container swapping techniques and streamlined host resource isolation.

### 4. Custom Security & Identity Integration
Developed a tailored OIDC/MSAL authentication service that bridges external B2B identity providers with an internal BI-backed RBAC system.
> **Outcome:** Successfully implemented a Zero-Trust approach, providing granular access control without sacrificing the performance of the underlying SQL Server 2016 instance.

---
*Created for portfolio purposes. Contact me for a detailed walkthrough of the architectural decisions behind this project.*
