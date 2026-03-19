# QlikSense Custom VCS & Deployment Orchestrator

> **Note on Confidentiality:** This project is a proprietary commercial application developed under a Non-Disclosure Agreement (NDA). To respect intellectual property rights, the source code is not publicly available. This documentation serves as a functional and architectural case study.

---

## 2. Project Overview
A containerized **.NET 6 Web API** designed to automate the CI/CD pipeline for Qlik Sense applications. The system serves as a specialized orchestration layer that bridges the gap between the BI environment and **Azure DevOps**. It dynamically prepares deployment packages by extracting load scripts and metadata, feeds them into version control, and triggers automated push processes to promote assets across Test and Production environments.

---

## 3. The Challenge (Problem Statement)
* **The Issue:** Qlik Sense applications are binary files (`.qvf`), which natively hide the backend logic from version control systems. Standard deployments were manual and lacked code-level visibility.
* **The Risk:** Deploying "black-box" binaries meant that logic changes could not be reviewed or audited, leading to high risk during production promotions and no way to "diff" script versions.

---

## 4. Proposed Solution & Logic Flow
The application acts as a pre-deployment engine that standardizes how BI assets are prepared and versioned before they enter the Azure DevOps pipeline.

---

### Key Features:
* **Automated Asset Preparation:** Before publishing, the service interfaces with the Qlik Engine API to extract the backend load script as a text file, ensuring every binary deployment is accompanied by human-readable code.
* **VCS Feed Logic:** Dynamically manages the "Commitment Feed," gathering app metadata and scripts to feed into Azure DevOps Repos.
* **Trigger-Based Push Process:** Once the environment is prepared, the service programmatically triggers Azure DevOps pipelines to execute the final push to target streams.
* **13-Point Operation Suite:** A robust set of backend actions (Publish, Copy, Sync, Unpublish) that handle the complex movement of apps between Work Areas and official streams.

### Tech Stack:
* **Backend:** .NET 6 Web API (C#)
* **Orchestration:** Azure DevOps REST API (Repos & Pipelines)
* **BI Integration:** Qlik Engine API (WebSocket) & QRS API (REST)
* **Environment:** Docker (Linux Containerized)

---

## 6. Key Achievements & Impact
* **Code Visibility:** Enabled code-level versioning for BI for the first time by converting hidden load scripts into versionable text files.
* **Deployment Reliability:** Achieved a **100% reduction** in manual scheduling conflicts through automated state management.
* **Auditability:** Every production push is now backed by a transparent commit history in Azure DevOps, showing exactly what changed in the ETL logic.
* **Infrastructure Efficiency:** By containerizing the orchestrator in Docker, the deployment process remains consistent across all development and production agents.


---

*Created for portfolio purposes. Contact me for a detailed walkthrough of the architectural decisions behind this project.*