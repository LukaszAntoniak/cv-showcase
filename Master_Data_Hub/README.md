# Master Data Hub

> **Note on Confidentiality:** This project is a proprietary commercial application developed under a Non-Disclosure Agreement (NDA). To respect intellectual property rights, the source code is not publicly available. This documentation serves as a functional and architectural case study.

---

## 🛡️ Business Context
The Master Data Hub is a specialized data-governance application designed to sanitize and formalize the onboarding of new vendors, facilitate their removal, and ensure all existing records remain up-to-date. By acting as a mandatory quality-control gate, it ensures that all supplier metadata is validated and legally protected before being committed to the corporate ERP environment.

* **Lifecycle Management:** Manages the end-to-end supplier journey, from initial onboarding to decommissioning and removal.
* **Data Integrity:** Acts as the "Single Source of Truth," ensuring that updates to vendor details are synchronized and accurate.
* **Data Quality Assurance:** Implements strict client-side validation rules per divisions to prevent "dirty data" (invalid Tax IDs, malformed IBANs) from entering the ERP.
* **Document Management:** Leverages SharePoint’s native capabilities to handle sensitive supplier attachments and signed contracts.

---

## 🛠️ Tech Stack
* **Frontend Rendering:** Mustache.js (Rendering engine).
* **Core Logic:** Vanilla JavaScript.
* **Backend & API:** SharePoint REST API / OData.
* **Storage:** SharePoint Lists & Document Libraries (Attachments).
* **Authentication:** SharePoint 2013 On Premises / Azure AD (Single Sign-On).
* **Styling:** CSS3 (Custom-built for SharePoint fluid integration).

---

## 🧠 Key Decisions & "Why"
* **Mustache.js for Rendering:** Chosen to provide a high-performance, lightweight UI experience without the overhead or versioning conflicts of heavy frameworks.
* **SharePoint as a Headless DB:** It leverages native SharePoint versioning and audit trails—features that remain easily manageable by the back-office department via standard lists.
* **Client-Side "Data Quality" Engine:** Validation is performed in real-time within the JS Controller. This provides immediate feedback to users, ensuring 100% compliance with ERP data schemas before submission.
* **Integrated File Handling:** Using SharePoint's native attachment capabilities ensures that sensitive supplier documents (Bank confirmations) are stored in a secure, encrypted environment with existing backup policies.

---

## 🚀 Key Achievements (Impact)
1.  **Enhanced Integrity & Anti-Fraud:** The "Data Quality Shield" serves as a critical gatekeeper, enforcing strict validation and business logic that eliminated manual data rework and mitigated the risk of fraudulent entries.
2.  **Streamlined Onboarding:** Integrated NDA signing reduced the average supplier setup time.
3.  **Zero Infrastructure Footprint:** By hosting the app and data within SharePoint, the project utilizes the existing resources.

---

*Created for portfolio purposes. Contact me for a detailed walkthrough of the architectural decisions behind this project.*