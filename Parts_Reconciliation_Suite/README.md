# Logistics Reconciliation Engine

> **Note on Confidentiality:** This project is a proprietary internal tool developed under an NDA. To respect intellectual property rights, the source code is not publicly available. This documentation serves as a technical case study on high-volume data orchestration.

---

## 2. Project Overview
A headless **.NET 6 Web API** designed to automate the synchronization and reconciliation of global inventory data. The system aggregates logistics data from disparate sources—including legacy SharePoint 2013 reports, FTP file servers, and MS SQL databases—to generate a "Single Source of Truth" master report on **SharePoint Online**.

---

## 3. The Challenge (Problem Statement)
* **Collaboration Conflict:** The final report is a "living" Excel document on SharePoint Online where multiple human stakeholders enter manual adjustments. Automated updates risked overwriting human input.
* **Data Fragmentation:** Warehouse state data was scattered across legacy Excel files, SQL tables, and external 3PL (3rd Party Logistics) FTP feeds.
* **Inaccuracy:** Discrepancies between the internal ERP and the 3PL provider led to "phantom inventory," causing logistics delays and financial errors.

---

## 4. Proposed Solution & Logic Flow
I built a "Smart Sync" engine that doesn't just overwrite files, but merges state data while preserving human collaboration.


### Key Features:
* **Multi-Source ETL (Extract, Transform, Load):** * **Legacy Extraction:** Scrapes data from legacy SharePoint 2013 Excel reports.
    * **External Feeds:** Parses raw inventory files from 3PL providers via FTP.
    * **Database Aggregation:** Queries MS SQL Server for real-time ERP warehouse states.
* **Intelligent Synchronization Logic:** Instead of a simple "upload," the API downloads the current SharePoint Online master file, performs a delta-comparison, and updates only the necessary cells. This allows the Excel file to serve as a **collaboration platform** for humans while receiving automated data injections.
* **Warehouse State Reconciliation:** Automatically flags discrepancies where the ERP state does not match the 3PL provider state across multiple divisions.
* **Headless Observability:** As this app has no UI, it relies heavily on my **Custom NLog Library**, feeding execution status and "Reconciliation Success" metrics into the **BI Resource Monitor**.

### Tech Stack:
* **Backend:** .NET 6
* **File Processing:** ClosedXML / OpenXML (for high-performance Excel manipulation)
* **Security:** Azure Enterprise Application (Client Credentials Flow) for SharePoint Online access.
* **Infrastructure:** Docker Container / Windows Task Scheduler (Environment dependent).

---

## 6. Key Achievements & Impact
* **Inventory Transparency:** Provided a real-time view of warehouse states across multiple global divisions for the first time.
* **Human-Machine Collaboration:** Successfully implemented a system where an Excel file serves as both a database for an API and a UI for human stakeholders.
* **Operational Accuracy:** Reduced manual data entry by ~15 hours per week and eliminated the risk of human error during data aggregation.
* **Automated Audit Trail:** Every sync is logged, providing a history of inventory changes that previously went untracked.

---

## 7. Lessons Learned
* **Technical:** Managing the complexity of the SharePoint Online Graph API vs. legacy CSOM when handling large Excel workbooks.
* **Business:** Designing "Conflict Resolution" logic—determining which data source (ERP or 3PL) takes precedence during a reconciliation mismatch.

---
*Created for portfolio purposes. Contact me for a detailed walkthrough of the architectural decisions behind this project.*