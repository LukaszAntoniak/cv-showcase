# Bunker Room Scheduler

> **Note on Confidentiality:** This project is a proprietary commercial application developed under a Non-Disclosure Agreement (NDA). To respect intellectual property rights, the source code is not publicly available. This documentation serves as a functional and architectural case study.

---

## 💼 Business Context: R&D Resource Scheduling & Workflow
A specialized Resource Planning (ERP-lite) system designed to manage the high-security logistics of testing bunkers and product validation labs.

* **High-Fidelity Scheduling Interface:** Features a sophisticated interactive calendar designed for desktop power users to manage complex, long-term testing rotations.

* **Multi-Stage Approval Pipeline:** Orchestrates the transition from engineer request to facility manager verification, ensuring all high-security protocols are met before a booking is finalized.

* **Administrative Metadata Engine:** Includes a robust "No-Code" module that allows managers to dynamically reconfigure room parameters and form requirements on the fly.

* **Resource Throughput Optimization:** Maximizes the utilization of high-cost facilities by eliminating scheduling overlaps and providing clear visibility into lab bottlenecks.

---

## 🛠️ Tech Stack & Skills
* **Backend:** .NET 6 (Containerized), ASP.NET Core API.
* **Frontend:** React (SPA), MSAL.js, HashRouter, Static Assets Deployment.
* **Identity & Security:** OAuth2 / OpenID Connect (OIDC), MS Entra ID (B2B), Custom Token Management Service, CORS Policy Management.
* **Infrastructure:** IIS (Internet Information Services), URL Rewrite Module, Docker, Windows Server 2019.
* **Database:** MS SQL Server 2016 (Bare-Metal).


## 🧠 Key Decisions & "Why"
* **Containerized .NET Core API:**
  * *Why:* Ensures 100% parity between local testing and the production Windows Server environment, simplifying the deployment of complex scheduling updates.
* **Custom Identity Redirect Pattern:**
  * *Why:* By decoupling the authentication logic into a separate subsite, we centralized the MSAL configuration, making it reusable across multiple BI and R&D portals while keeping the core app "Identity Aware" but not "Identity Burdened."
* **Mobile-Optimized Availability View:**
  * *Why:* Field engineers needed quick, low-latency access to room status while physically present in the lab areas, leading to a dedicated "Mobile-First" UI path.
* **Dynamic Form Configuration:**
  * *Why:* Testing requirements change per product line; allowing administrators to modify the request form ensures the system remains flexible without requiring developer intervention.

---

## 🚀 Key Achievements (Impact)
1. **Optimized Resource Management:** Streamlined the end-to-end booking lifecycle and a 100% reduction in manual scheduling conflicts.
2. **Data-Driven Insights:** Integrated a performance tracking layer that delivers real-time effectiveness KPIs, providing leadership with actionable data on bunker utilization and facility ROI.
3. **Enterprise-Grade Security:** Fortified the system by integrating corporate B2B identity providers (SSO), ensuring that sensitive testing schedules and high-security facility data are restricted to authorized personnel only.
3. **Operational Agility:** Empowered facility managers through a dynamic "No-Code" administration engine, allowing them to customize workflows and room parameters instantly to meet changing project demands.


---

*Created for portfolio purposes. Contact me for a detailed walkthrough of the architectural decisions behind this project.*
