# Project Closure

> **Note on Confidentiality:** This project is a proprietary commercial application developed under a Non-Disclosure Agreement (NDA). To respect intellectual property rights, the source code is not publicly available. This documentation serves as a functional and architectural case study.

---

## 🛡️ Business Context
The Project Closure Hub is a specialized workflow application designed to formalize the decommissioning and final settlement of corporate projects. It orchestrates a mandatory approval chain across key departments, ensuring every project meets operational and financial requirements before final closure.

* **Cross-Functional Approvals:** Automates the sign-off process between Finance, Sales, and Service departments.
* **Financial Governance:** Ensures all billings and payments are reconciled before the project number is formally deactivated.
* **Centralized Status Tracking:** Provides a single source of truth for all projects in the closure phase.
* **Unified BI Integration:** Leverages the collocated Data Warehouse to provide real-time financial validation directly within the closure workflow.

---

## 🛠️ Tech Stack
* **Backend:** .NET Framework, ASP.NET MVC.
* **Frontend:** Razor Pages, Kendo UI (jQuery/MVC).
* **Background Processing:** .NET Worker Service (Windows Service).
* **Orchestration:** SQL Server Agent (Job Scheduling).
* **Identity:** Windows Authentication (SSO), Kerberos, Active Directory (AD).
* **Unified Database:** MS SQL Server (Bare-metal hosting App DB & BI/DWH).

---

## 🧠 Key Decisions & "Why"
* **Unified SQL Server Instance:** By hosting the BI/DWH and App DB on a single bare-metal server, the system achieves maximum data throughput and simplifies complex cross-schema joins.
* **Kerberos Implementation:** Windows Authentication was chosen for seamless SSO and to leverage existing Active Directory group structures for role-based access.
* **Separation of Concerns (Worker Service):** Heavy data preparation is offloaded to a background service to keep the web interface responsive during financial data refreshes.
* **SQL Server Agent Orchestration:** Provides a reliable, native mechanism to trigger the Worker Service 3x daily without external dependencies.

---

## 🚀 Key Achievements (Impact)
1. **High-Performance Data Access:** Collocating BI and Application data on a single bare-metal instance reduced report generation time by 40%.
2. **Security & SSO:** Implemented a Zero-Touch login experience for users via Kerberos.
3. **Automated Synchronization:** Ensured 100% data consistency for Finance teams through the automated 3x daily refresh cycle.

---

*Created for portfolio purposes. Contact me for a detailed walkthrough of the architectural decisions behind this project.*